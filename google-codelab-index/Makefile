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

CLOSURE_COMPILER := /Users/sbusolits/.closure/closure-compiler-v20181028.jar
SOY_COMPILER := /Users/sbusolits/.closure/SoyToJsSrcCompiler.jar

JS_SRCS = $(shell find . -name '*.js' ! -name '*_test.js' ! -path './bin/*')
SOY_SRCS = $(shell find . -name '*.soy' ! -path './bin/*')
SOY_JS = $(shell find . -name '*.js' -path './bin/soy/*')

OUT_BIN_DIR := ./bin/js
OUT_SOY_DIR := ./bin/soy

bin: google_codelab_index_bin.js

# The flags that include closure-tempaltes should specify the javascript folder
# under closure-templates, but that breaks a requirement for
# goog.soy.SanitizedStyle. That's only provided in a testdata file in the
# codelabs-templates repo - I have no idea where we're actually supposed to get
# it from.
google_codelab_index_bin.js: templates $(JS_SRCS)
	mkdir -p $(OUT_BIN_DIR)
	java -jar $(CLOSURE_COMPILER) --js=$(JS_SRCS) \
	    --entry_point 'googlecodelabs.CodelabIndexDef' \
	    --only_closure_dependencies \
	    --js='./bin/soy/**.js' \
	    --js='../../../closure-library/**.js' \
	    --js='!../../../closure-library/**_test.js'  \
	    --js='../../../closure-templates/javascript/**.js' \
	    --js='!../../../closure-templates/javascript/**_test.js'  \
	    >$(OUT_BIN_DIR)/$@

templates: $(SOY_SRCS)
	mkdir -p $(OUT_SOY_DIR)
	java -jar $(SOY_COMPILER) \
	    --shouldProvideRequireSoyNamespaces \
	    --outputPathFormat '$(OUT_SOY_DIR)/{INPUT_FILE_NAME_NO_EXT}_template.js' $^

clean:
	rm -rf ./bin