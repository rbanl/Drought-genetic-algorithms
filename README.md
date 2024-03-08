I built a  genetic algorithm model in MATLAB that simulated the evolution of optimal trade-offs that led to optiimal drought resistance. This evolution took place to droughts occurring - a condition mimicking our current environment. My experiment replicated this  across environments that had increasing levels of droughts.



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
