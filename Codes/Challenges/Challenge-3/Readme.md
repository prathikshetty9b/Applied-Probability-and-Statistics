# **Three Doors**

## **Problem Statement**


A game show has the following setup: there are 3 doors, say A, B, and, C. Behind one random door is a prize, and behind the other two doors, there is nothing. The game participant is asked to select a door first. After that, the game host opens one among the other two doors  (that the participant has not selected) behind which is empty. Now the participant is offered the choice to switch (between the door that has been selected and the one that the host has not opened). If you are the participant, would you switch or not? 


```R
# Sampling space 
s = c('D1','D2','D3');

# Corresponding Probabilities
p = (1/3) *c(1,1,1)


#pickDoor = sample(s ,size = 1, replace = FALSE, prob = p )
#pickDoor


#priceDoor = sample(s, size = 1, replace = FALSE, prob = p)
#priceDoor

#First Row indicates Participants Choice , Second Row indicates Winning Door
nsimulations = 1e6
simulatedData = replicate(nsimulations,sample(s, size = 2 , replace = TRUE, prob = p)) 

#We already know that host will choose a door without prize

#Liklihood of him winning if he sticks to his decision 
checkEventWin1 = function(data) {
    if(data[1] == data[2])
    {
        return(1) 
    }
    return(0) 

}

mean(apply(simulatedData,2,checkEventWin1))

#Liklihood of him winning if he switches doors 
checkEventWin2 = function(data) {
    if(data[1] != data[2])
    {
        return(1) #switch if participant didn't choose the winning door 
    }
    return(0) #don't switch if participant chose the winning door
}

mean(apply(simulatedData,2,checkEventWin2))
```


0.333822



0.666178

