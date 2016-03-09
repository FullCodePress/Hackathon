# March Madness Hackathon
# Full Code Press


myFile=open('MasterData.csv','r')
other32list=[]
autoList=[]

for line in myFile:
	if 'CONFERENCE' not in line:
		myString= line.split(',')
		
		#parse out information
		school=myString[0]
		conf=myString[1]
		conf_dif_rank=myString[2]
		rank_in_conf=myString[3]
		games_won=myString[4]
		past_wins=myString[5]
		
		#calculate score
		conf_dif_rank_score=33-int(conf_dif_rank)
		rank_in_conf_score=int(rank_in_conf)-1
		score=conf_dif_rank_score-rank_in_conf_score+int(games_won)+int(past_wins)
		
		#if school is ranked 1 in its conference
		if rank_in_conf=='1':
			autoList.append([school,conf,score]) 
		
		#get top 32 teams not ranked 1
		else:
			other32list.append([school, conf, score])

myFile.close()

#pull top 32 from the other schools list
other32sorted=sorted(other32list, key=lambda tup: tup[2], reverse=True)
finalother32srt=other32sorted[0:32]

#merge list to create bracket of 64
mergeList = autoList + finalother32srt

#sort merge list to attain seeding
mergeList.sort(key=lambda tup: tup[2], reverse=True)

#write to file
printed32=open('other32sorted.txt','w')
for line in mergeList:
	printed32.write("%s\n" %line)
printed32.close()




	
