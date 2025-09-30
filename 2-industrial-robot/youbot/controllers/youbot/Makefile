# Youbot controller Makefile (self-contained, cross-platform)

# If WEBOTS_HOME not set by Webots GUI, try to autodetect
ifeq ($(WEBOTS_HOME),)
  ifeq ($(OS),Windows_NT)
    # On Windows, guess Program Files install (adjust if needed)
    WEBOTS_HOME := C:/Program Files/Webots
  else
    # On Linux or macOS, try 'which webots'
    WEBOTS_BIN := $(shell which webots 2>/dev/null)
    ifneq ($(WEBOTS_BIN),)
      WEBOTS_HOME := $(dir $(WEBOTS_BIN))..
    else
      # fallback
      WEBOTS_HOME := /Applications/Webots.app/Contents
    endif
  endif
endif

WEBOTS_HOME_PATH := $(strip $(WEBOTS_HOME))

include $(WEBOTS_HOME_PATH)/resources/Makefile.include

C_SOURCES = youbot.c
INCLUDE  += -I"$(WEBOTS_HOME_PATH)/include/controller/c"

RESOURCES_PATH = $(WEBOTS_HOME_PATH)/projects/robots/kuka/youbot
INCLUDE   += -I"$(RESOURCES_PATH)/libraries/youbot_control/include"
LIBRARIES += -L"$(RESOURCES_PATH)/libraries/youbot_control" -lyoubot_control

EXECUTABLE = youbot
