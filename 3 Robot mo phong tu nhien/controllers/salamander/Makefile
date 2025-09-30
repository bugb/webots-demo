# Salamander controller Makefile (portable + auto mkdir)

# --- Detect WEBOTS_HOME ---
ifeq ($(WEBOTS_HOME),)
  ifeq ($(OS),Windows_NT)
    WEBOTS_HOME := C:/Program Files/Webots
  else
    WEBOTS_BIN := $(shell command -v webots 2>/dev/null)
    ifneq ($(WEBOTS_BIN),)
      # on macOS: .../Webots.app/Contents/MacOS/webots → go up two levels
      WEBOTS_HOME := $(abspath $(dir $(WEBOTS_BIN))/..)
    endif
    ifeq ($(WEBOTS_HOME),)
      WEBOTS_HOME := /Applications/Webots.app/Contents
    endif
    ifeq ($(wildcard $(WEBOTS_HOME)/resources/Makefile.include),)
      ifneq ($(wildcard /usr/local/webots/resources/Makefile.include),)
        WEBOTS_HOME := /usr/local/webots
      endif
    endif
  endif
endif

# Normalize: if user pointed to app root, add /Contents
ifeq ($(wildcard $(WEBOTS_HOME)/resources/Makefile.include),)
  ifneq ($(wildcard $(WEBOTS_HOME)/Contents/resources/Makefile.include),)
    WEBOTS_HOME := $(WEBOTS_HOME)/Contents
  endif
endif

# Final guard
ifeq ($(wildcard $(WEBOTS_HOME)/resources/Makefile.include),)
  $(error Could not locate Webots Makefile.include. Set WEBOTS_HOME to your install. Tried: '$(WEBOTS_HOME)')
endif

WEBOTS_HOME_PATH := $(abspath $(WEBOTS_HOME))

# --- Pull Webots build rules (ONCE only) ---
include $(WEBOTS_HOME_PATH)/resources/Makefile.include

# --- Sources and includes ---
C_SOURCES = salamander.c
INCLUDE  += -I"$(WEBOTS_HOME_PATH)/include/controller/c"

# --- Executable name ---
EXECUTABLE = salamander

# --- Build mode (release by default) ---
BUILD_MODE ?= release

# --- Ensure build dirs exist ---
BUILD_DIRS := build/$(BUILD_MODE)/x86_64

$(BUILD_DIRS):
	$(MKDIR) -p $@

# Hook dirs into object file builds
$(EXECUTABLE): $(BUILD_DIRS)

# --- Explicitly link Controller lib ---
LIBRARIES += -L"$(WEBOTS_HOME_PATH)/lib/controller" -lController
