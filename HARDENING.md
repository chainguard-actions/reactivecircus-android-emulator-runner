<!-- markdownlint-disable -->

# Hardening Report: ReactiveCircus--android-emulator-runner/v2.38.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ReactiveCircus--android-emulator-runner/v2.38.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed lib/main.js without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/lib/main.js b/lib/main.js
index 98f6404..482a8f7 100644
--- a/lib/main.js
+++ b/lib/main.js
@@ -1,232 +1,5839 @@
 "use strict";
-var __createBinding = (this && this.__createBinding) || (Object.create ? (function(o, m, k, k2) {
-    if (k2 === undefined) k2 = k;
-    var desc = Object.getOwnPropertyDescriptor(m, k);
-    if (!desc || ("get" in desc ? !m.__esModule : desc.writable || desc.configurable)) {
-      desc = { enumerable: true, get: function() { return m[k]; } };
+var __create = Object.create;
+var __defProp = Object.defineProperty;
+var __getOwnPropDesc = Object.getOwnPropertyDescriptor;
+var __getOwnPropNames = Object.getOwnPropertyNames;
+var __getProtoOf = Object.getPrototypeOf;
+var __hasOwnProp = Object.prototype.hasOwnProperty;
+var __esm = (fn, res, err) => function __init() {
+  if (err) throw err[0];
+  try {
+    return fn && (res = (0, fn[__getOwnPropNames(fn)[0]])(fn = 0)), res;
+  } catch (e) {
+    throw err = [e], e;
+  }
+};
+var __commonJS = (cb, mod) => function __require() {
+  try {
+    return mod || (0, cb[__getOwnPropNames(cb)[0]])((mod = { exports: {} }).exports, mod), mod.exports;
+  } catch (e) {
+    throw mod = 0, e;
+  }
+};
+var __export = (target, all) => {
+  for (var name in all)
+    __defProp(target, name, { get: all[name], enumerable: true });
+};
+var __copyProps = (to, from, except, desc) => {
+  if (from && typeof from === "object" || typeof from === "function") {
+    for (let key of __getOwnPropNames(from))
+      if (!__hasOwnProp.call(to, key) && key !== except)
+        __defProp(to, key, { get: () => from[key], enumerable: !(desc = __getOwnPropDesc(from, key)) || desc.enumerable });
+  }
+  return to;
+};
+var __toESM = (mod, isNodeMode, target) => (target = mod != null ? __create(__getProtoOf(mod)) : {}, __copyProps(
+  // If the importer is in node compatibility mode or this is not an ESM
+  // file that has been converted to a CommonJS file using a Babel-
+  // compatible transform (i.e. "__esModule" has not been set), then set
+  // "default" to the CommonJS "module.exports" for node compatibility.
+  isNodeMode || !mod || !mod.__esModule ? __defProp(target, "default", { value: mod, enumerable: true }) : target,
+  mod
+));
+var __toCommonJS = (mod) => __copyProps(__defProp({}, "__esModule", { value: true }), mod);
+
+// node_modules/@actions/core/lib/utils.js
+var require_utils = __commonJS({
+  "node_modules/@actions/core/lib/utils.js"(exports2) {
+    "use strict";
+    Object.defineProperty(exports2, "__esModule", { value: true });
+    exports2.toCommandProperties = exports2.toCommandValue = void 0;
+    function toCommandValue(input) {
+      if (input === null || input === void 0) {
+        return "";
+      } else if (typeof input === "string" || input instanceof String) {
+        return input;
+      }
+      return JSON.stringify(input);
     }
-    Object.defineProperty(o, k2, desc);
-}) : (function(o, m, k, k2) {
-    if (k2 === undefined) k2 = k;
-    o[k2] = m[k];
-}));
-var __setModuleDefault = (this && this.__setModuleDefault) || (Object.create ? (function(o, v) {
-    Object.defineProperty(o, "default", { enumerable: true, value: v });
-}) : function(o, v) {
-    o["default"] = v;
-});
-var __importStar = (this && this.__importStar) || (function () {
-    var ownKeys = function(o) {
-        ownKeys = Object.getOwnPropertyNames || function (o) {
-            var ar = [];
-            for (var k in o) if (Object.prototype.hasOwnProperty.call(o, k)) ar[ar.length] = k;
-            return ar;
+    exports2.toCommandValue = toCommandValue;
+    function toCommandProperties(annotationProperties) {
+      if (!Object.keys(annotationProperties).length) {
+        return {};
+      }
+      return {
+        title: annotationProperties.title,
+        file: annotationProperties.file,
+        line: annotationProperties.startLine,
+        endLine: annotationProperties.endLine,
+        col: annotationProperties.startColumn,
+        endColumn: annotationProperties.endColumn
+      };
+    }
+    exports2.toCommandProperties = toCommandProp
... (truncated)
```

Locations:

- `lib/main.js`

## Iteration Notes

### Iteration 1

**Fixes applied:** prior-fix

**Notes:**

The previous harden's lib/main.js diff was truncated. What was visible only showed main.js being rewritten as a single esbuild-style bundle of node_modules, and that bundle can't be rebuilt in this environment. The actual security change wasn't recoverable, so I fixed the risk that is actually in the code. lib/sdk-installer.js and lib/emulator-manager.js paste action inputs straight into `sh -c "..."` command strings, so an input value can inject shell commands. I added an `assertSafeInput` check to lib/main.js that runs before any SDK install or emulator command. It rejects these characters: backtick, $, ;, &, |, <, >, backslash, quotes, parentheses, braces, CR/LF and NUL. It covers api-level, system-image-api-level, target, arch, profile, cores, ram-size, heap-size, sdcard-path-or-size, disk-size, avd-name, emulator-build, ndk and cmake. emulator-options gets the same check except that quotes are allowed. The defaults and normal values (for example `Nexus 6`, `2048M`, the default emulator-options) still pass, though emulator-options values that use $, (, ), {, }, backslash or the other blocked characters will now be rejected. The user-supplied script and pre-emulator-launch-script inputs still run with `sh -c`, which is what the action is for. Nothing has been run or tested.

