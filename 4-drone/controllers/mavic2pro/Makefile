# Copyright 1996-2023 Cyberbotics Ltd.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Webots Makefile system
#
# You may add some variable definitions hereafter to customize the build process
# See documentation in $(WEBOTS_HOME_PATH)/resources/Makefile.include


# Do not modify the following: this includes Webots global Makefile.include
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
C_SOURCES = mavic2pro.c
INCLUDE  += -I"$(WEBOTS_HOME_PATH)/include/controller/c"

# --- Executable name ---
EXECUTABLE = mavic2pro

# --- Build mode (default release) ---
BUILD_MODE ?= release

# --- Ensure build dirs exist ---
BUILD_DIRS := build/$(BUILD_MODE)/x86_64
$(BUILD_DIRS):
	$(MKDIR) -p $@

$(EXECUTABLE): $(BUILD_DIRS)

# --- Explicitly link Controller lib (needed on macOS) ---
LIBRARIES += -L"$(WEBOTS_HOME_PATH)/lib/controller" -lController
