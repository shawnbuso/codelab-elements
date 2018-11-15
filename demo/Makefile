# Copyright 2016 Google Inc. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

CLOSURE_LOC := /Users/sbusolits/.closure/closure-compiler-v20181028.jar

SRCS = $(shell find . -name '*.js' ! -name '*_test.js' ! -path './bin/*')

OUTDIR := ./bin

bin: hello_bin.js

hello_bin.js: $(SRCS)
	mkdir -p $(OUTDIR)
	java -jar $(CLOSURE_LOC) --js=$^ \
	    --entry_point 'googlecodelabs.HelloElement' >$(OUTDIR)/$@

clean:
	rm -rf $(OUTDIR)/*