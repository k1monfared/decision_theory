# This algorithm assumes that boys propose and girls decide, which according to Gale-Shapley ends up in the best possible stable situation for all boys and worst possible stable situation for all girls. If you want to switch, simply switch the list of boys and girls when calling the main function, no need to edit any of the code!

# The Find(List, String) function looks into the List and returns the index of the first occurence of the String.
# Each entry of the list itself is a list of length two. Find0 finds the String among first entries, and Find1 finds the Strings among second entries.

def Find0(List,String):
    for i in range(len(List)):
        if String == List[i][0]:
            return(i)
        
    return('none')

def Find1(List,String):
    for i in range(len(List)):
        if String == List[i][1]:
            return(i)
        
    return('none')
    
########################################################

# Shuffle(List) takes the List and shuffles it.
# This is just used in to avoid manually making a preference list for each person

def Shuffle(List):
    n = len(List)
    tempList= [ [random(),List[i]] for i in range(n)]
    tempList.sort()
    
    finalList = [[tempList[i][1],0] for i in range(n)]
    #I added that zero after each name which means they are-not-proposed-to/have-not-proposed yet
    
    return(finalList)
    
#########################################################

# Propose() does today's round of proposals.

def Propose(Girl, Boy, GirlsPreferences, BoysPreferences):
    # Good morning, let's make some proposals today
    n = len(Girl)
    P = [] # this is a list of today's proposals, what? no one has proposed yet? Quich get ready, get the guys!
    i=0 # strat from the first guy
    j=0 # start from the first girl in his list
    while i < n: # Go to each boy in the list
        while j < n: # Go down their list in order
            if BoysPreferences[i][j][1] >= 0: # If the girl is not rejected him yet
                BoysPreferences[i][j][1] = 1  # then propose to her
                P += [BoysPreferences[i][j][0]] # Add this girl to the list of today's proposals
                r = Find0(GirlsPreferences[P[i]],i) # Find the girl in the girls list
                GirlsPreferences[P[i]][r][1] = 1 # Let the girls know she is proposed to
                i += 1 # go to next boy in the list
                j=0 # start from the beginning of his list
                if i == n: # If everyone has proposed for today
                    return # stop
            else: # If the girls has rejected him
                j += 1 # go to next girl in his list

#############################################################

# Accept() does today's round of acceptance of proposals.

def Accept(Girl, Boy, GirlsPreferences, BoysPreferences, G): # Well well, it's around dinner time and girls have got tons of proposals from their lovers, let's who are the lucky guys today
    n = len(Girl)
    for i in range(n): # Start with the first girl
        for j in range(n): # Go down her list
            if GirlsPreferences[i][j][1] == 1: # Is she proposed by this guy? If yes
                if j <= G[i][1]: # is he at least as good as her current husband? If yes
                    G[i][1] = j # Accept him
                else: # If he's not better than her current husband
                    GirlsPreferences[i][j][1] = -1 # Reject him
                    r = Find0(BoysPreferences[GirlsPreferences[i][j][0]],i) # Find the guy in the list of the boys
                    BoysPreferences[GirlsPreferences[i][j][0]][r][1] = -1 # Let him know he is rejected
                    
########################################################################

# This part gives a visual presentation of the current situation. I'm gonna call this after each proposal and after each acceptance (i.e. twice a day)

def drawTables(Girl, Boy, GirlsPreferences, BoysPreferences):
    
    n = len(Girl)
    TableG = text('Received', (0,1/2), rgbcolor = (0,0,0))
    TableG += line([(-1/2,1/4), (n+1/2,1/4)], rgbcolor = (0,0,0))
    TableG += line([(1/2,3/4), (1/2,-n/2+1/4)], rgbcolor = (0,0,0))
    
    TableB = text('Proposed', (0,-n/2-1+1/2), rgbcolor = (0,0,0))
    TableB += line([(-1/2,-n/2-1+1/4), (n+1/2,-n/2-1+1/4)], rgbcolor = (0,0,0))
    TableB += line([(1/2,-n/2-1+3/4), (1/2,-n/2-n/2-1+1/4)], rgbcolor = (0,0,0))
    
    for i in range(n):    
        TableG += text('C %s' %(i+1), (i+1,1/2), rgbcolor = (0,0,0))    
        TableG += text(Girl[i], (0,-i/2), rgbcolor = (0,0,0))
   
        for j in range(n):
            d = 0
            c = (0,0, 102/255) # Everyone in the list is blue
            if GirlsPreferences[i][j][1] == 1:
                c = (0, 153/255, 0) # If you're accepted, then you are green
                TableG += ellipse(((j+1),-i/2),1/2,1/4, rgbcolor = c)
                
            elif GirlsPreferences[i][j][1] == -1:
                c = (1,0,0) # If you are rejected, then you are red
                TableG += line([((j+1)-1/3,-i/2-1/8), ((j+1)+1/3,-i/2+1/8)], rgbcolor = c)
                TableG += line([((j+1)-1/3,-i/2+1/8), ((j+1)+1/3,-i/2-1/8)], rgbcolor = c)
                
            TableG += text(Boy[GirlsPreferences[i][j][0]], ((j+1),-i/2), rgbcolor = c)

    for i in range(n):    
        TableB += text('C %s' %(i+1), (i+1,-n/2-1+1/2), rgbcolor = (0,0,0))    
        TableB += text(Boy[i], (0,-n/2-1+-i/2), rgbcolor = (0,0,0))
   
        for j in range(n):
            d = 0
            c = (0,0, 102/255) # Everyone in the list is blue
            if BoysPreferences[i][j][1] == 1:
                c = (0, 153/255, 0) # If you're accepted, then you are green
                TableB += ellipse(((j+1),-n/2-1-i/2),1/2,1/4, rgbcolor = c)
                
            elif BoysPreferences[i][j][1] == -1:
                c = (1,0,0) # If you are rejected, then you are red
                TableB += line([((j+1)-1/3,-n/2-1-i/2-1/8), ((j+1)+1/3,-n/2-1-i/2+1/8)], rgbcolor = c)
                TableB += line([((j+1)-1/3,-n/2-1-i/2+1/8), ((j+1)+1/3,-n/2-1-i/2-1/8)], rgbcolor = c) 
                
            TableB += text(Girl[BoysPreferences[i][j][0]], ((j+1),-n/2-1-i/2), rgbcolor = c)
        
    (TableG + TableB).show(figsize=[n/2+4, n/2+2],axes=False)
    
######################################################

# And here is where I put all of it together which is essentially the main part of the algorithm

def find_stable_marriages(HowMuch, Girl, Boy, GirlsPreferences='none', BoysPreferences='none'):
    # Girl is a list of names of the girls
    # Boy is a list of names of boys
    # GirlsPreferences is a list of n lists, each containing numbers 0,1,...,n-1 exactly ones
    # BoysPreferences is a list of n lists, each containing numbers 0,1,...,n-1 exactly ones
    # If HowMuch = 0, it only prints the final result, otherwise it prints everyday's result
        
    n = len(Girl)
    
    if GirlsPreferences == 'none': # If you don't give a preference list, this makes a random one
        GirlsPreferences = [Shuffle([i for i in range(n)]) for i in range(n)]
    
    if BoysPreferences == 'none': # If you don't give a preference list, this makes a random one
        BoysPreferences = [Shuffle([i for i in range(n)]) for i in range(n)]
        
    # This bit is just to clear all history to run the algorithm over the same set of data without reshuffling it!    
    for i in range(n):
        for j in range(n):
            GirlsPreferences[i][j][1]=0
            BoysPreferences[i][j][1]=0

    G = [] # G is the list of girls and their current husbands, with default = n, since they are not proposed by anyone yet, so they only have a hypothetical husband.
    for i in range(n):
        G.append( [Girl[i], n])
    
    
    M = [0 for i in range(n)] # This is 1 if guy i is married
    
    d = 0 # Day zero, it shows a list of girls and boys and their preference lists
    if HowMuch != 0:
        print('Day %s' %d)
        drawTables(Girl, Boy, GirlsPreferences, BoysPreferences)
    
    while M != [1 for i in range(n)]: # while there is a single guy
        d += 1 # Go to next day
        
        Propose(Girl, Boy, GirlsPreferences, BoysPreferences) # Boys propose
        if HowMuch != 0:
            print('Day %s Proposals' %d)
            drawTables(Girl, Boy, GirlsPreferences, BoysPreferences) # Show the situation
        

        Accept(Girl, Boy, GirlsPreferences, BoysPreferences, G) # Girls accept or reject
        if HowMuch != 0:
            print('Day %s Acceptances' %d)
            drawTables(Girl, Boy, GirlsPreferences, BoysPreferences) # Show the situation
        
        M = [ max( [ BoysPreferences[i][j][1] for j in range(n)  ] ) for i in range(n) ]   # Check to see which guy is still single.
        
    if HowMuch == 0:
        print('Final decision made after %s days:' %d)
        drawTables(Girl, Boy, GirlsPreferences, BoysPreferences) # Show the situation
######################################################
######################################################


######################################################
# And a sample run:
        
Girls = ['Charlotte','Elizabeth','Jane','Lydia'] #names of girls
Boys = ['Bingley','Collins','Darcy','Wickhem'] #names of boys

find_stable_marriages(1,Girls, Boys) # that 1 tells me I want to see the resaults of everyday, If you just want to see the final decision change it into 0

#######################################################

# A sample run where the preferences are not random

G = ['Charlotte','Elizabeth','Jane','Lydia'] #names of girls
GP = [[[0, 0], [1, 0], [2, 0], [3, 0]], [[3, 0], [2, 0], [1, 0], [0, 0]],
[[0, 0], [3, 0], [2, 0], [1, 0]], [[0, 0], [3, 0], [2, 0], [1, 0]]] # this is how to define a preferece list

B = ['Bingley','Collins','Darcy','Wickhem'] #names of boys
BP = [[[1, 0], [0, 0], [3, 0], [2, 0]], [[2, 0], [1, 0], [3, 0], [0, 0]],
[[2, 0], [0, 0], [3, 0], [1, 0]], [[0, 0], [3, 0], [2, 0], [1, 0]]]

find_stable_marriages(0,G, B, GP, BP) # that 1 tells me I want to see the results of everyday, If you just want to see the final decision change it into 0
#######################################################

# Another sample run with more boys and girls

n = 10

Girls = [ 'Girl '+'%s' %(i+1) for i in range(n) ] #names of girls
Boys = [ 'Boy '+'%s' %(i+1) for i in range(n) ] #names of boys

find_stable_marriages(0,Girls, Boys) 

###########################################################

# Another sample run by fixing the preferences list and then running it once as guys propose, and once as girls propose

#Here I'm going to compare two results if boys propose, and if girls propose

n = 10

G = [ 'Girl '+'%s' %(i+1) for i in range(n) ] #names of girls
B = [ 'Boy '+'%s' %(i+1) for i in range(n) ] #names of boys

# So I'm gonna fix a preference list first 
GP = [Shuffle([i for i in range(n)]) for i in range(n)]
BP = [Shuffle([i for i in range(n)]) for i in range(n)]



find_stable_marriages(0, G, B, GP, BP) # Here boys propose
find_stable_marriages(0, B, G, BP, GP) # Here girls propose

# Note that if the results of the both are the same, that means there's only one possible stable situation.
