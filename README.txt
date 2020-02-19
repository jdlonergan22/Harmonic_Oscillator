Simple classical harmonic oscillator represented with monte carlo metropolis algorithm - diatomic molecules only 

Adjustable parameters: 
    Temperature (T - units are K) - the higher the temperature the greater the probability of reaching higher energy states
    Number of iterations (n) - more iterations the closer the energy and length values reach the equilibrium values 
    Mass of atom 1 in 2 atom molecule (m1 - units are amu) - default value is mass of H atom 
    Mass of atom 2 in 2 atom molecule (m2 - units are amu) - default value is mass of H atom 
    Wavenumber of molecule (L - units are m^-1) - default value is for H2 molecule
    
Note energy and displacement at each step are stored in the pandas dataframe titled "df"
    
Wavenumber is the spacial frequency of a wave measured in cycles/unit distance. For example 350cm^-1 means wave completes 1 cycle/350cm

To calculate the change in energy from the equilibrium position, measure E = 0.5 * k * L^2 where k is the bond force constant and L is the displacement from the equilibrium position. 

Note that the bond force constant (k) is equivalent to the spring constant in Hooke's Law and is calculated by be the relationship 
w = sqrt(k/u) where w is the angular frequency and u is the reduced mass of the diatomic molecule. w is found by multipling the linear frequency (wavenumber * speed of light = linear frequency) by 2pi. 



=> Steps of MC Metropolis Algorithm: 

    1. Get random start position between -10 and 10 angstroms from equilibrium position. Calculate corresponding energy and store in datatable
    
    2. Generate random displacement from start position and calculate energy at potential move position 
    
    3. Compare potential move position energy with current position energy 
    
            a. If move position energy < current position energy 
            
                - Create new entry in data table for new energy level and displacement from   equilibrium length. 
                
            b. If move position energy > current position energy 
                
                - Generate random probability value between 0 and 1
                
                - calculate probability value* of move from current position to move position (higher energy level)
                
                - if random probability > calculated then don't accept move and copy most recent data entry into new row in dataframe
                
                - if random probability < calculated then accept move and store new energy and length value into new row in dataframe

    4. Repeat steps 2 and 3 for n iterations 
    
    5. Calculate mean from dataframe for energy and length - with more iterations, it should approach zero 
    
    
    
*Calculating probability value via Boltzmann distribution: 
    - p = exp(-(potential step energy - current energy)/(Boltzmann's constant * temeperature)) 


Note on calculating probability value via Boltzmann distribution: Sometimes in the calculations you may get to an energy level on the order of around 10^-20 eV and then move to level of 10^-3 eV. This appears to be a large jump in energy due to an order of magnitude change around +20. However, this change in energy is still relatively low (change of about 10^-3 eV) and in turn the p value can be significant and the move to the higher energy level can be accepted.
                
                
Note on 3rd graph produced: 
Colors represent density of data points on graph: 
    - dark blue means less dense (fewer iterations at this energy level and bond length) 
    - yellow to red means more dense (more iterations at this energy level and bond length)
                
                
                
                
                
                
                
