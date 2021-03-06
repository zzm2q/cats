// This file contains the build logic for CATS

var fs = require("fs");
var path = require("path");

var workerOptions = [
   "src/typings/typescript.d.ts",
   "src/typings/cats.d.ts",
   "src/tsworker/languageservicehost.ts",    
   "src/tsworker/isense.ts"
];

var umlOptions = [
   "--target ES5",
   "src/typings/arbor.d.ts",
   "src/typings/jsuml2.d.ts",
   "src/uml/layout.ts"
];

var catsOptions = [
    "--target ES5",
    "src/typings/ace.d.ts",
    "src/typings/cats.d.ts",
    "src/typings/jsuml2.d.ts",
    "src/typings/node-webkit.d.ts",
    "src/typings/typescript.d.ts",
    "src/cats/promise.ts",
    "src/cats/infobus.ts",
    "src/cats/os.ts",
    "src/cats/observable.ts",
    "src/cats/treewatcher.ts",
    "src/cats/ide.ts",
    "src/cats/layout.ts",
    "src/cats/acesession.ts",
    "src/cats/commands/commander.ts",
    "src/cats/commands/editorcommands.ts",
    "src/cats/commands/filecommands.ts",
    "src/cats/commands/helpcommands.ts",
    "src/cats/commands/idecommands.ts",
    "src/cats/commands/navigatecommands.ts",
    "src/cats/commands/projectcommands.ts",
    "src/cats/commands/refactorcommands.ts",
    "src/cats/configloader.ts",
    "src/cats/editor.ts",
    "src/cats/isensehandler.ts",
    "src/cats/menu/editorcontextmenu.ts",
    "src/cats/menu/filecontextmenu.ts",
    "src/cats/menu/menubar.ts",
    "src/cats/menu/tabcontextmenu.ts",
    "src/cats/project.ts",
    "src/cats/ui/autocompleteview.ts",
    "src/cats/ui/elemtabadapter.ts",
    "src/cats/ui/grid.ts",
    "src/cats/ui/mvc.ts",
    "src/cats/ui/tabbar.ts",
    "src/cats/ui/tooltip.ts",
    "src/cats/ui/tree.ts",
    "src/cats/pane/toolbar.ts",
    "src/cats/pane/compilationresults.ts",
    "src/cats/pane/navigator.ts",
    "src/cats/pane/outline.ts",
    "src/cats/pane/searchresults.ts",
    "src/cats/pane/statusbar.ts",
    "src/cats/pane/tasklist.ts",
    "src/cats/main.ts"
];


/**
 * Compiler task
 */
task('compile', {async:true}, function(outFile, options) {
		var cmd = "tsc --out " + outFile + " " + options.join(" ") ;

		// console.log(cmd + "\n");
		var ex = jake.createExec([cmd]);
		
		// Add listeners for output and error
		ex.addListener("stdout", function(output) {
			process.stdout.write(output);
		});
		ex.addListener("stderr", function(error) {
			process.stderr.write(error);
		});
		ex.addListener("cmdEnd", function() {
		    var time = new Date();
            var stamp = time.toLocaleTimeString();
			console.log(stamp + " done creating file " + outFile);
			complete();
		});
		ex.addListener("error", function() {
			fs.unlinkSync(outFile);
			console.log("Compilation of " + outFile + " unsuccessful");
		});
		ex.run();	
});


// Set the default task
task("default", function() {
   jake.Task['compile'].invoke("lib/main.js", catsOptions);
   jake.Task['compile'].invoke("lib/tsworker.js", workerOptions);
   jake.Task['compile'].invoke("lib/uml.js", umlOptions);
});


