Bickle (because one of these days hes going to get organazized)
==============================================================

organise related async actions into a single group



	var myGroup = Bickle.create({

		
		initialize : function() {
		
			/* runs first - synchronous */
			
			return { time : (new Date()).hours };
		},
		
		actions : {
			
			// entry point - asynchronous
			actionOne : {
				
				// will do these first 
				dependencies : Bickle.dependsOn('actionTwo, actionThree'),
				
				// results is an object containing the combined results of the dependencies
				work : function(args, results) {
					
					var newValue = results.actionTwo.integerValue * results.actionThree;
					
					console.log('start time :: ' + args.time;
					
					API.getStuffFromServer(newValue, function(resultFromServer) {
					
						Linearise.returns(resultFromServer);
					});
				}
			},
			
			actionTwo : {
				
				// all work items receive the original args from the initialize as the first argument
				work : function(args) {
				
					API.getStuffFromServer(function(resultFromServer) {
					
						Bickle.returns(resultFromServer);
					});
				}
			},

			actionThree : {
							
				work : function(args) {
				
					API.getStuffFromServer(function(resultFromServer) {
					
						Bickle.returns(resultFromServer);
					});
				}
			
			}			
		},
		
		finalize : function(args, finalResult) {
		
			/* runs at end when all actions are complete. return is return value of myGroup */
			
			return finalResult.filename;
		}

	});



use	
---

	myGroup.exec(function(results) {
	
		/* everything has happened  */	
	});


	
