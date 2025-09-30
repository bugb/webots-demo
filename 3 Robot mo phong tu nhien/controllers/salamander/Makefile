# Paste this at the top of each controller Makefile
# ----- Portable Webots include header (GUI + CLI, macOS/Linux/Windows) -----

# 0) If WEBOTS_HOME already provided (by Webots GUI or user), keep it.
#    Otherwise try to autodetect.
ifeq ($(WEBOTS_HOME),)
  ifeq ($(OS),Windows_NT)
    # Common default on Windows (adjust if your install is different)
    WEBOTS_HOME := C:/Program Files/Webots
  else
    # Try to locate the webots binary
    WEBOTS_BIN := $(shell command -v webots 2>/dev/null)
    ifneq ($(WEBOTS_BIN),)
      # On macOS it's .../Webots.app/Contents/MacOS/webots → go up one level
      # On Linux it’s usually /usr/local/webots/bin/webots → go up two levels
      # The “..” here works for macOS; Linux will be normalized below.
      WEBOTS_HOME := $(abspath $(dir $(WEBOTS_BIN))..)
    endif
    # Fallback for macOS DMG install
    ifeq ($(WEBOTS_HOME),)
      WEBOTS_HOME := /Applications/Webots.app/Contents
    endif
    # Common Linux fallback
    ifeq ($(wildcard $(WEBOTS_HOME)/resources/Makefile.include),)
      ifneq ($(wildcard /usr/local/webots/resources/Makefile.include),)
        WEBOTS_HOME := /usr/local/webots
      endif
    endif
  endif
endif

# 1) Normalize macOS “.app root” to “…/Contents” if user pointed at the app root
ifeq ($(wildcard $(WEBOTS_HOME)/resources/Makefile.include),)
  ifneq ($(wildcard $(WEBOTS_HOME)/Contents/resources/Makefile.include),)
    WEBOTS_HOME := $(WEBOTS_HOME)/Contents
  endif
endif

# 2) Final guard – fail early with a clear message if we still can’t find it
ifeq ($(wildcard $(WEBOTS_HOME)/resources/Makefile.include),)
  $(error Could not locate Webots Makefile.include. Set WEBOTS_HOME to your install. Tried: '$(WEBOTS_HOME)')
endif

# 3) Now include Webots’ rules
include $(WEBOTS_HOME)/resources/Makefile.include

$(shell mkdir -p build/release/x86_64 build/debug/x86_64 >/dev/null)

# (Optional) expose a convenience var the rest of your Makefile can use
WEBOTS_HOME_PATH := $(WEBOTS_HOME)
null :=
space := $(null) $(null)
WEBOTS_HOME_PATH?=$(subst $(space),\ ,$(strip $(subst \,/,$(WEBOTS_HOME))))
include $(WEBOTS_HOME_PATH)/resources/Makefile.include

C_SOURCES = salamander.c
INCLUDE  += -I"$(WEBOTS_HOME_PATH)/include/controller/c"
EXECUTABLE = salamander
