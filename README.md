I built a  genetic algorithm model in MATLAB that simulated the evolution of optimal trade-offs that led to optiimal drought resistance. This evolution took place to droughts occurring - a condition mimicking our current environment. My experiment replicated this  across environments that had increasing levels of droughts.

Different physiological traits require the same limited resources to function. For resource optimization, organisms evolve to allocate a shared resource to different trait involved in a trade-off and usually in an even manner. Some traits are not precisely determined and their fitness can vary due to them being easily negatively affected, this is trait uncertainty. I reproduced results from (Currey, Pitchford and Baxter, 2006) using a genetic algorithm (GA), an evolution simulator. For mineral optimization in bones there is a trade-off between making a bone stiff or tough. Using the GA, uncertainty in toughness was altered. For mineral optimization, increased uncertainty in different experiments led to greater proportions of minerals being allocated to stiffness. The frequency and severity of droughts is set to increase. Plants use drought-avoidance strategies during droughts. These include increasing root aquaporin expression and the recruitment of Arbuscular Mycorrhizha fungi to build deeper hyphal networks. These strategies stabilise plants’ water status. Both strategies require carbon to function, therefore for there is a trade-off occurring. The fungi strategy was the uncertain one. How droughts alter carbon optimization as uncertainty was increased was measured. Adding and increasing drought frequencies reduced the effect of how carbon optimization changed. In certain circumstances, this optimization involved developing a genotype to allocate more greater carbon proportions to aquaporin expression, the certain trait. Other features such as periodic drought occurrences would allow the GA’s code to mimic natural drought occurrences better and could potentially and slightly increase the applicability of the results.



# Methods
3.1 Genetic algorithm 
To know if the principle stated above applied to the bone system and the plant system and to get results, I had to simulate the evolutionary process of natural selection on a computer to find an optimal solution to a trade-off. A very simple genetic algorithm (GA) was used. GAs are standard techniques used in various fields to find optimal solutions to scenarios with trade-offs (McCall, 2005). My GA was simple as it contained no genetic cross over and no sexual reproduction between the parents. Simulation of the GA was performed in MATLAB R2021a. The GA used for the bone and plant models contained the following features:
Reproduction
Parents reproduced asexually - each parent generated 10 offspring, each of which had DNA inherited from their respective parent. 
Mutational noise
Mutational noise (∆) was a randomly generated number between 0 and 1, generated in each generation. Out of all the offspring, each offspring will be given 1 number from this randomly generated set of numbers. Each offspring’s Δ was calculated by multiplying 0.05 with the randomly generated number given to it. This product would be added to the genotypic value in each offspring.
Inheritance
Each offspring inherited DNA with a genotypic value from its parent. The inherited DNA in each offspring was inherited by adding the inherited genotypic value to mutational noise. Where g is any offspring’s genotype and gp is the offspring’s parent’s genotype, the genotype of any particular offspring is given by the following equation:
g = gp + (∆) (Equation 1)
Population 
Each generation had a population of 100 parents and 1000 offspring.
Fitness function
This was reproduced from (Currey, Pitchford and Baxter, 2006). It is assumed that an organism has a genotype m. The amount of mineralization in bones may be between 0 and 1. The m causes the organism to use a certain amount of mineral for stiffness or toughness, therefore m governs an individual’s fitness with respect to (w.r.t) pre-yield stiffness and post-yield toughness of bones. Stiffness and toughness were represented respectively by S and T. S is proportional to m and T is proportional to (1 - m). An optimal m creates a trade-off between stiffness and toughness. Given all the information above, fitness can be assumed to be: 
F= m(1-m) (Equation 2) 
Fitness in equation 2 is an imprecise genetic description and is only used to quantify the likelihood that an individual will survive and move into the next generation. Due to the nature of T, which has uncertainty, the T value is a random variable proportional to (1 – m + ξ). Different individuals would have different ξ values so, an individual’s fitness would be:
F= m(1-m + ξ ) (Equation 3) 
Uncertainty
Uncertainty / genotypic-phenotypic noise, which was described in the introduction, is a factor producing ξ. ξ is a random value affecting the fitness of T. In the code a spread of ξ values were produced. From this set of values produced, a particular ξ value was added into the fitness function of each individual, to produce a fitness in each individual.  This occurred in every generation. Uncertainty was equated to unc in the GA, and in attempts to alter the spread/variability of the ξ set of values which are used to produce fitnesses, unc was varied five times from 0 to 0.5, with an interval of 0.1, as it was done in section 4c in (Currey, Pitchford and Baxter, 2006). At each different unc, the GA was run to produce a set of genotypes called the final parental genotypic values.
Final parental genotypic values
A single run of the GA produced a set of final parental genotypic values. In this set, each individual had a genotypic and a phenotypic value. These values were stored in a variable. At any particular uncertainty, I got 5 means of each set of final parental genotypic values that were produced from repeating the run with the exact same parameters. These means from the 5 different runs with the same parameters were stored in a variable. I also got a mean of means of these 5 means and stored it in a variable. This was done because when the model was run repetitively, between different runs, the final parental genotypic values and hence their averages varied. This mean of means was denoted by m*.
Selection pressure 
In every generation there was a selection pressure. The offspring with the highest fitness values survived and were selected to move into the next generation. Only 10% of the offspring were selected to move into the next generation. In the last generation the offspring are selected based on their fitness values calculated from their genotypic values.

Generations
Both GA models contained 100 generations. In both models, each generation was complete after DNA was inherited by each offspring from each parent, each offspring expressed their fitnesses which was then potentially selected which would determine their potential survival.
Steps in the genetic algorithm
1.A set of initial parents with a set of random genetic values, with each parent having their own genotypic value assigned to them from this set of values.
2.These parents produced a fitness using the fitness function in the code.
3.These parents were selected according to their fitnesses.
4.Parents that were selected were allowed to move into the next generation.
5.These parents produced offspring.
6.Each of these offspring inherited DNA from their respective parents with genotypic noise
7.Offspring become parents and the process from step 2 repeats   itself until a final generation of offspring are produced.
8. From this final generation, only the fittest offspring were used for analysis.
3.2 Addition of droughts to the GA code
Everything mentioned above remained the same. To adapt the model, I made a few changes. The code was designed so that any generation that employed the use of the drought fitness function represented a drought year. The employment of a different fitness function with different genotypes could be considered analogous to changes in phenotypes due to epigenetic changes occurring. The expression of an epigenome leads to a different gene expression pattern which in turn leads to a different phenotype (Weinhold, 2006). In this case it is thought that the epigenetic changes which are rapid, could occur in response to droughts. Normal years were simulated by use of non-drought fitness function mentioned earlier in (equation 2). The plant trade-off GA model featured a random number generator function that occurred in each generation. This number did or did not satisfy a condition. If the condition was met, then the non-drought code was run. The code was altered so that this condition was met a certain number of times so in the GA’s simulated generations there would be 33%,66% and 99% generations containing droughts. Different experiments contained different amounts of droughts. Progressive increases of drought frequencies were used in an attempt to understand the effect of increasing number of droughts. The code was altered so at each unc, in all the different drought frequency experiments, the mean of each set of final parental genotypes was calculated. 20 sets of final parental genotype were calculated at each unc in all the different drought frequency experiments. A mean of these means was calculated, this was called c*. This was done to increase reliability. 
In (Manzoni et al., 2013), “Sapwood hydraulic conductivity is the product of the water potential and xylem hydraulic conductivity. As in (Manzoni et al., 2013), both drought-avoidance traits contribute to the same function, and following the ideas in (Currey, Pitchford and Baxter, 2006) it makes sense to consider a fitness function defined by the product of the 2 drought-avoidance strategies. Water is an essential component for many essential reactions and processes like photosynthesis and plant growth, so it is a limiting factor for plant survival. Nutrients such as phosphorous and nitrogen are also essential to plants’ fitness and are decreased during droughts (Bista et al., 2018). It is important to note that water is decreased the most during droughts. As water content decreases the most and it is essential to fitness, in drought conditions, fitness may be measured by water content. Both drought-avoidance traits contribute to water uptake and maintaining the plant’s water status. The trade-off being used is only speculative and this report is primarily concerned with the effect unc has on evolution in different conditions. In the GA, it is the magnitude of an individual’s fitness that determines whether it moves into the next generation. Fitness being determined primarily by the two drought-avoidance traits would make it simpler to characterise the effects of the traits on evolution. Code with greater complexity – code having more variables might be more realistic but it will make disentangling the effect unc in the traits has on the results more complex.
Similar to the ideas in (Currey, Pitchford and Baxter, 2006), when one trait is uncertain and another is certain, increased aquaporin expression was the certain strategy and hyphal networks built by AM fungi was the uncertain strategy. A plant has a genotype c that governs a plant’s fitness with respect to root aquaporin and water absorbing hyphal networks produced by AM fungi. Genotype c determines how much carbon is proportioned for the functioning of that trait. The fitness resulting from aquaporin expression and AM-fungal hyphal network depth have the respective notations of AQP and AM. The amount of carbon a plant has available for use in any given year:
CTotal = CAM  + CAQP  (Equation 4)
As fitness is a product of AQP and AM, equation 5 is as follows:
F=AQP(AM) (Equation 5)
This report speculates that during droughts, plants will develop a genotype shown by equation 6 where it increases a much greater proportion of carbon is allocated to AM fungi, so the AM fungi can build deeper hyphal networks for more water uptake. Carbon is limited, so this will lead to a trade-off involving a reduced amount of carbon that a plant can use for aquaporin regulation. AQP is proportional to (0.3c) and AM is proportional to ( 1.7(1-c)+ ξ). It is possible that 0.3 and 1.7 could both be different, but this is only a speculative trade-off. This will lead to the following equation:  168 748 4.45  171 731   4.2  174  714 4.1
F=(0.3c)( 1.7(1-c)+ ξ) (Equation 6)
When rearranged, equation 6, which occurs during droughts leads to a lower fitness than a fitness produced from the equation representing normal years, considering there is no change in ξ between the 2 equations. Drought-avoidance strategies are used to maintain a plant’s water status, but not necessarily increase a plant’s water content. During droughts there is less water so a plant’s water status will be maintained only at a lower level. As water content is used as a proxy for fitness in this report, a lower plant water status / content leads to a lower fitness.
It is also important to note that equation 2 was used in the bones trade-off as well as in the speculative plant trade-off to produce a fitness in normal years. Equation 2 is taken from (Currey, Pitchford and Baxter, 2006) and is only a formula for the case where an individual’s total fitness is a product of its genotypes. This equation is not specific for the bones trade-off, so it can be used with different traits.




#PLEASE SEE CODE BELOW:
genmax = 100; %generations for the GA
nbones = 100; % number of individuals
noffspring = 15; % number of offspring per individual

xi = 0.05; % genotype-to-phenotype noise
mnoise = 0.05; % mutational noise

parents = rand(1,nbones); % set the parents' phenotypes
offspring = zeros(2,nbones*noffspring); % matrix to store the offspring

for gen = 1:genmax   % loop through the generations
    icount = 0;
    for foindiv = 1:nbones   % loop through each parent
        offspring(1,(1+(icount*noffspring)):((icount*noffspring))+noffspring) = parents(foindiv) + mnoise*(rand(1,noffspring)-0.5); % inherit parent's genotype with noise
        offspring(2,:) = offspring(1,:).*(1 - offspring(1,:));
        icount = icount + 1;
    end
end
