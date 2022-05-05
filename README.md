// Mirza Baig
// MATH3020 - Probability & Statistics
import java.util.Random;
import java.util.Arrays;
//Test on IntelliJ or Eclipse
class Simulation {
 public static void main(String[] args) {
 int computers = 20; // number of computers in the network
 int r = 5; // max number of computers cleaned daily
 double p = 0.1; // probability of spreading the virus
 double currentlyInfected = 0;
 boolean endFlag = false;
 int simulations = 100000;
 int[] averageLog = new int[simulations];

 for (int y = 0; y < simulations; y++) {
  int time = 1;
  // Initially computer #0 is infected (set to 1),
            // computers #1 thru #19 are clean (set to 0).
  int[] comps = new int[computers];
  comps[0] = 1;
  
  for(int i = 1; i < computers; i++) {
    comps[i] = 0;
    }
   //System.out.println(Arrays.toString(comps));
    while (endFlag == false) {
     // For each wire "infected -> noninfected":
    // perform a Bernoulli trial with probability p=0.1;
      // if success, computer #j becomes newly_infected (set to 2).
     for(int i = 0; i < computers; i++) {
       for(int j = 0; j < computers; j++) {
         if ((comps[i] == 1) && (comps[j] == 0)) {
         int x = MyBernoulli(p);
         if (x == 1) {
             comps[j] = 2;
       }
      }
   }
 }
  // After that, mark all newly_infected as simply infected.
  for(int i = 0; i < computers; i++) {
     if (comps[i] == 2) {
        comps[i] = 1;
        currentlyInfected++;
        }
    }
  //System.out.println(Arrays.toString(comps));
   //Afternoon sequence
  //If infected <= 5, end round of simulation (all clean)
     if (currentlyInfected <= 5) {
      System.out.println("Day 0 Clean");
       break;
   }
 //If infected > 5, select 5 random infected computers for cleaning
     else {
      int cleanCount = 5;
      for(int i = 0; (i < computers) && (cleanCount != 0); i++) {
      if(comps[i] == 1) {
         comps[i] = 0;
         currentlyInfected--;
         cleanCount--;
           }
     }
         time++;
       }
  }
      System.out.println("Day " + time + ": " + currentlyInfected + " computers infected, " + "expected computers that gets infected once is " + currentlyInfected/p + "%");
      averageLog[y] = time;
    }
      System.out.println(Arrays.toString(averageLog));
      double total = 0;
      for(int i = 0; i < averageLog.length; i++) {
         total = total + averageLog[i];
       }
      double average = total / averageLog.length;
      System.out.println("The average is " + average + " days ");
    }
 
    public static int MyBernoulli(double p) {
      double U = Math.random();
      int X;
     if (U < p) {
         X = 1;
        }
     else {
       X = 0;
        }
        return X;
    }
}
