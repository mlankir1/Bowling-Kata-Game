# Bowling-Kata-Game

public class Game
{   
    static boolean isSpare = false, isStrike = false;
    static int[][] frameCount = new int[10][2];
    static int i = 0, j = 0, bonus = 0, score = 0;
    static int[] a1 = new int[10];
    static int[] a2 = new int[10];
    static int count1 = 0, count2 = 0;

    public static void main(String args[]) {
        for(int k=0;k<10;k++){
            a1[k]=0; a2[k]=0;
        }
System.out.println("Start bowling.. (Keep entering pin count)");
        for (i = 0; i <10; i++) {
            int pinsLeft = 0;
            for (j = 0; j <2; j++) {
                System.out.println("Frame: " + (i + 1) + "  Trial: " + (j + 1));
                try {
                    int z = 10 - frameCount[i][0];
                    int pinCount = Integer.parseInt(System.console().readLine());
                    if (pinCount < 0 || pinCount > 10) {
                        j--;
                        System.out.println("Please enter number between 0 to 10");
                        continue;
                    } else if (j == 1 && (frameCount[i][0] + pinCount) > 10) {
                        j--;
                        System.out.println("How can you make " + pinCount + " pins fall, when there are only " + z + " pins left.");
                        continue;
                    } else {
                        frameCount[i][j] = pinCount;
                        if (j == 1) {
                            if (pinCount == 10) isStrike = true;
                        } else {
                            if (pinCount - z == 0 && isStrike!=true) isSpare = true;
                        }


                        roll(pinCount);
                    }


                } catch (NumberFormatException nfe) {
  j--;
                    System.out.println("Please enter a proper number");
                    continue;
                }


            } // j loop
         if(i==9) score();
        } // i loop


    }


    public static void roll(int pins) {

        if (isStrike == true) {
            j++;
            System.out.println("STRIKE");
            if(i!=9)
            isStrike = false;
            a2[count2] = j;
            count2++;
            System.out.println(a2[count2]);
        }
        if (isSpare == true) {
            j++;
            System.out.println("SPARE");
            if(i!=9)
            isSpare = false;
            a1[count1] = i + 1;
            count1++;
            System.out.println(frameCount[a1[count1]][0]);
        }
        score += pins;
    }

    public static void score() {
            if(isStrike == true || isSpare == true){
                int p[]=new int[3];
            System.out.println("Wow, you can roll extra balls with 3 maximum chances. Go ahead");
            for(int m=0;m<2;m++){
            int zCount = Integer.parseInt(System.console().readLine());
            if(zCount<0 || zCount>10) System.out.println("Please enter number between 0 to 10");
            else { roll(zCount); 
            int d=0;
                for(int n=0;n<m;n++)
                    d+=p[n];
                    if(d>=10)
                m=2;
                else d=0;
            
            }
            }
            }
        for(int i=0;i<10;i++){
            bonus+= frameCount[a1[i]][0];
            for(int j=0;j<2;j++)
                bonus+=frameCount[a2[j]][0];
        }
            score+=bonus;
        System.out.println("Your total score is: " + score);
  }
}
