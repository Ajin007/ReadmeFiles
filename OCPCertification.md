1. Problem one
     ```
        class MathFunctions{
        
        public static void addToInt(int a, int amountToAdd){
            a = a + amountToAdd;
        }
        
        public static void main(String[] arg){
            var a =15;
            var b=10;
            MathFunctions.addToInt(a,b);
            System.out.println(a); // answer will be 15 
            
        }
    }

  2. Problem 2
  ```
  // the first error of the code occur in the new object area since we can not create new object for the abstract class
        interface HasTail {
        int getTailLength();
    }
    
    abstract class Puma implements HasTail{
        protected int getTailLength(){
            return 4;
        }
        
    }
    
    class Cougar implements HasTail{
        
        
        public static void main(String arg[]){
            var puma=new Puma();
            System.out.println(puma.getTailLength());
            
        }
        
        public int getTailLength(int length){
            return 2;
        }
    }

```
3. problem 3
   ```
    public static void main(String[] arg){
     
    int moon = 9, star = 2 + 2 * 3;
    float sun = star>10 ? 1 : 3;
    double jupiter = (sun + moon) - 1.0f;
    int mars = --moon <= 8 ? 2 : 3;
    System.out.println(sun+"-"+jupiter+"-"+mars);    //3.0-11.0-2
4. problem 
