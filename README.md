SetList
=======
/**
 * Author: James Dinh
 * Date: 12/31/2014
 * Purpose: Quickly obtaining an ArrayList<Integer> using an RNG instead of user input
 */
import java.util.ArrayList;
import java.util.Random;

public class SetListIntegers
{
  // instance variables
  private static Random rng = new Random();
  
  // Get values into the list
  public static ArrayList<Integer> setList(ArrayList<Integer> list)
  {
    int sizeMax = 450;
    int sizeMin = 50;
    int maxValue = 500;
    int minValue = 1;
    // the list Size will be an RNG value of sizeMin-sizeMax
    int listSize = rng.nextInt(sizeMax - sizeMin + 1) + sizeMin;
    System.out.println("list size: " + listSize);
    int element; // element holds the RNG value
    boolean isDuplicate = false; // Used to prevent duplicate numbers
    ArrayList<Integer> usedNumberStorage = new ArrayList<Integer>(); // List to hold previous, unique values of the RNG to prevent duplicates
    
    // Loop that adds values to the list
    for (int counter = 0; counter < listSize; counter++)
    {
      element = rng.nextInt(maxValue - minValue + 1) + minValue; // RNG rolls a number from minValue-maxValue
      // duplicate check does not need to run for the first iteration
      if (counter != 0)
      {
        // This block is to prevent duplicate numbers from showing up
        do
        {
          // if a previous element is a duplicate
          // re-roll element
          if (isDuplicate)
          {
            element = rng.nextInt(maxValue) + minValue;
          }
          // compares RNG value to all values in the number storage
          for (int count = 0; count < usedNumberStorage.size(); count++)
          {
            // Once a duplicate is found
            // flip isDuplicate to true
            // and break out of the for-loop
            if (element == usedNumberStorage.get(count))
            {
              isDuplicate = true;
              break;
            } else
            {
              // if no duplicate is found, exit the do-while
              isDuplicate = false;
            }
          }
        } while (isDuplicate); // as long as the RNG value roll matches a previous roll, run the check
      }
      list.add(element); // Adds the RNG value to the list
      usedNumberStorage.add(element); // Collects previous unique values of the RNG
      if (usedNumberStorage.size() == (maxValue - minValue + 1))
      {
        System.out.println("List size exceeds number of possible values.Terminating prematurely.");
        System.out.println("Excess number of list spaces: " + (listSize - (maxValue - minValue + 1)));
        break;
      }
    }
    return list;
  }
  
setArray
=======
// For Array
  public static int[] setArray(int[] list)
  {
    int maxValue = 500;
    int minValue = 1;
    int element; 
    boolean isDuplicate = false; 
    int[] usedNumberStorage = new int[maxValue - minValue + 1];
    int storageSize = 0;
    
    for (int counter = 0; counter < list.length; counter++)
    {
      element = rng.nextInt(maxValue - minValue + 1) + minValue;
      if (counter != 0)
      {
        do
        {
          if (isDuplicate)
          {
            element = rng.nextInt(maxValue - minValue + 1) + minValue;
          }
          for (int count = 0; count < storageSize; count++)
          {
            if (element == usedNumberStorage[count])
            {
              isDuplicate = true;
              break;
            } else
            {
              isDuplicate = false;
            }
          }
        } while (isDuplicate); 
      }
      list[counter] = element;
      usedNumberStorage[counter] = element;
      storageSize++;
      if (storageSize == usedNumberStorage.length)
      {
        System.out.println("List size exceeds number of possible values.Terminating prematurely.");
        System.out.println("Excess number of list spaces: " + (list.length - (maxValue - minValue + 1)));
        break;
      }
    }
    return list;
  }
}
