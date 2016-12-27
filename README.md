# Calculate-Vote
Add a separate function to calculate the sums of the votes



calculateVotes();

we have to tally up the votes on a separate function because the vote weight is based on the current balance of each account,so we should recalculate the balances at every new block or event: 

# this function will execute automatically when every new block arrives: 

web3.eth.filter('latest').watch(function(e, result){
    if(!e) {
        calculateVotes();
    }
}); 


now you can call the node and execute the action with: 

var totalPro, totalAgainst, totalVotes;
function calculateVotes() {
    totalPro = 0;
    totalAgainst = 0;
    totalVotes = 0;
    Object.keys(voteMap).map(function(a) { 
        // call the function asynchronously 
        web3.eth.getBalance(a, function(e,r) {
            voteMap[a].balance = Number(web3.fromWei(r, 'finney'));
            if (voteMap[a].support)
                totalPro += parseFloat(voteMap[a].balance); 
            else
                totalAgainst += parseFloat(voteMap[a].balance);
            // do something cool with the results!            
        });            
    });
}

this looping in each of the voting addresses and getting their balance



