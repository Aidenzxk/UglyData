

## Part 1 Importing


counties_rmt <-read.csv("counties_rmt.csv")

#remove first column
counties_rmt <- counties_rmt[ ,-1]

#convert to rows
counties_rmt <- t(counties_rmt)

#convert to data frame
counties_rmt <- as.data.frame(counties_rmt)

#create variables for counties from rows
counties_rmt$county_names <- row.names(counties_rmt)

#Assign numbers for variables
row.names(counties_rmt) <- 1:nrow(counties_rmt)

#switch order of columns to be names/total/male/female or such
counties_rmt <- counties_rmt[ ,c(4,1:3 )]

#assign names to columns 
names(counties_rmt) <- c("county_names", "total", "male", "female")

#check if male+female = total (shows 16 Trues - all true)
counties_rmt$total == counties_rmt$male + counties_rmt$female
table(counties_rmt$total == counties_rmt$male + counties_rmt$female)

#show table
counties_rmt

##Part 1 The Basics Yet Still COntinued

#bind Monserrado urban and rural, combining totals into a new data frame called mont_pops
mont_pops <- cbind(county_names = "Montserrado", counties_rmt[11,2:4] + counties_rmt[12,2:4])

#delete previous rows
counties_rmt <- counties_rmt[-11:-12,]

#Reform rows so that they are in correct order
counties_rmt <- rbind(counties_rmt[1:10,], mont_pops, counties_rmt[11:14,])

#move 13-16 to 12-15
row.names(counties_rmt) <- 1:nrow(counties_rmt)

##Part 1: The Basics Yet Continued Even More

#change order of river gee and rivercess in counties_rmt
counties_rmt <- counties_rmt[c(1:12,14,13,15), ]

#make numbers line up again
#??

  #comparing whether totals are more in the src dataset
counties_src$SUM_TOTAL > counties_rmt$total  

#src-rmt totals
cbind(counties_src$CCNAME, counties_src$SUM_TOTAL - counties_rmt$total)

#Calculate female percentage in the src
counties_src$per_female <- counties_src$SUM_FEMALE / counties_src$SUM_TOTAL

#Calculate female percentage in the rmt
counties_rmt$per_female <- counties_rmt$female / counties_rmt$total

#compare female populations
female_comp <-counties_src$per_female - counties_rmt$per_female

#Density Comparison
counties_src$density <- counties_src$SUM_TOTAL /
  counties_src$Sq_km

#total population barplot for src graph
barplot(t(counties_src[,2]),
        main = "Total Population Comparison for SRC Graph", 
        names.arg=counties_src[,1],
        col=c("red"),
        las=2, #this rotates the county names 90 degrees
        cex.names=0.55 #decrease county name size by 55%
        )



#Totals Showing Men and Women
barplot(t(counties_src[ ,c(3:4)]),
        main = "Total Pop by Men & Women",
        names.arg=counties_src[ ,1],
        legend = c("men","women"),
        col=c("darkblue","red"),
        las=2,
        cex.names=0.55
)


# Deliverable 2

#Total Pop. of each county including indication of male and female counts

barplot(t(cbind(counties_src[ ,2],counties_rmt[ ,2])),
        main = "Total Population Comparison in SRC and RMT Graph",
        names.arg=counties_src[ ,1],
        beside=TRUE,
        legend = c("source","remote"),
        col=c("darkblue","red"),
        las=2,
        cex.names=0.55)

        


                

#Difference in percent female between source and remote pop.datasets
        barplot(t(cbind(counties_src$per_female,
                        counties_rmt$per_female)),
                main = "Percent of Female Population in Source and Remote Pop.",
                names.arg=counties_src[ ,1],
                beside=TRUE,
                legend = c("source","remote"),
                col=c("darkblue","red"),
                las=2,
                cex.names=0.55 )
#Difference in female pop between source and remote
        
barplot(t(female_comp),
        main = "% Difference in Female Pop. of SRC and RMT Graphs", 
        names.arg=counties_src[,1],
        col=c("red"),
        las=2, #this rotates the county names 90 degrees
        cex.names=0.55
)        
        
#Pop density in counties_src

barplot(t(counties_src$density),
        main = "Population Density per City in Source Data", 
        names.arg=counties_src[,1],
        col=c("purple"),
        las=2, #this rotates the county names 90 degrees
        cex.names=0.55 #decrease county name size by 55%
)
#Check Charts
# counties_rmt
# counties_src

