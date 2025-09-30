# YouBot controller build (C) — macOS

# Always point to .../Contents
WEBOTS_HOME ?= /Applications/Webots.app/Contents
WEBOTS_HOME_PATH := $(strip $(WEBOTS_HOME))

# Pull Webots rules (DO NOT append another /Contents)
include $(WEBOTS_HOME_PATH)/resources/Makefile.include

# Your sources
C_SOURCES = youbot.c

# Webots C headers
INCLUDE += -I"$(WEBOTS_HOME_PATH)/include/controller/c"

# Optional: YouBot demo lib bundled with Webots
RESOURCES_PATH = $(WEBOTS_HOME_PATH)/projects/robots/kuka/youbot
INCLUDE      += -I"$(RESOURCES_PATH)/libraries/youbot_control/include"
LIBRARIES    += -L"$(RESOURCES_PATH)/libraries/youbot_control" -lyoubot_control

# If the linker complains about Controller, add this:
LIBRARIES    += -L"$(WEBOTS_HOME_PATH)/lib/controller" -lController
