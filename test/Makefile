# Copyright (C) 2017-2018 Jerome Migne

# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

NAME = sha2_test

BIN = $(NAME)

VPATH = . ..

CXX = g++

STD = -std=c++11

CXXFLAGS = $(STD) -Wall -O3

LDLIBS = -lboost_unit_test_framework

SOURCES = test_runner.cpp sha2.cpp sha2_test.cpp

#---------------------------------------------------------

.PHONY: all rebuild clean

all: $(BIN)

rebuild:
	@make clean && make

clean:
	rm -f *.o; rm -f *.d

#---------------------------------------------------------

$(BIN): $(SOURCES:.cpp=.o)
	$(CXX) -o $@ $^ $(LDLIBS)

%.d: %.cpp
	@echo "Generating dependencies for" $<; \
	set -e; rm -f $@; \
	$(CXX) -MM $(CPPFLAGS) $(STD) $< > $@.temp; \
	sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.temp > $@; \
	rm -f $@.temp

ifeq (,$(filter $(MAKECMDGOALS), clean rebuild))
-include $(SOURCES:.cpp=.d)
endif
