Part 1:

int[] reversed(int[] arr)

Bug: As it iterates through the array, it starts overwriting the first half of the array with the second half, but when it gets to the second half, it's actually overwriting with elements that it already changed.

Failure-inducing input:
```
 @Test
    public void testReversedFailure() {
        int[] input = {1, 2, 3, 4, 5};
        int[] expected = {5, 4, 3, 2, 1};
        assertArrayEquals(expected, ArrayExamples.reversed(input));
    }
```
Input that doesn't induce a failure:
```
 @Test
    public void testReversedNoFailure() {
        int[] input = {};
        int[] expected = {};
        assertArrayEquals(expected, ArrayExamples.reversed(input));
    }
```
  Symptom:

  testReversedFailure test case would fail with an AssertionError because the expected output array is not equal to the actual output.
  ```
org.junit.ComparisonFailure: 
Expected :[5, 4, 3, 2, 1]
Actual   :[1, 2, 3, 4, 5]
```

  Before-and-after:
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i++) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
}
```
The fix addresses the issue by correctly assigning the elements from the original array arr into the newArray in reversed order.

Part 2:

grep:

-r or --recursive: This option allows grep to perform a recursive search, looking into every file under each directory, and all subsequent subdirectories.

Example 1:
```
grep -r "function" ./technical/
```
This command searches for the word "function" in all files within the ./technical directory and all of its subdirectories.

Output(cropped): 

./technical/government/Post_Rate_Comm/Cohenetal_RuralDelivery.txt:function. The Commission found in the most recent omnibus rate case
./technical/government/Post_Rate_Comm/Cohenetal_RuralDelivery.txt:from the delivery function. We have estimated them for purposes of
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:The delivery function is comparatively new to modern postal
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:question: Do the economies of scale in the delivery function exceed
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:function. It then compares this benefit with the cost that the
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:function.
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:delivery function and the street delivery function. The former is
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:into the delivery sequence. "Delivery function" as used in this
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:economies of scale exist in the delivery of mail.8 Other functional
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:function because a single firm can deliver to a recipient at a
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:mail processing and transportation functions in the Postal
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:function.
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:"piggybacked" on all three functions.
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:The coverage function shown in Figure 1 models the change in the

Example 2:
```
grep --recursive "define" ./technical/
```
This command recursively searches for the string "define" within files located in ./technical and its subdirectories.

Output(cropped): 

./technical/plos/journal.pbio.0020311.txt:        each hormone have been defined largely by the application of exogenous hormone. More
./technical/plos/journal.pbio.0020311.txt:        defined by these mutations, coupled with expression studies aimed at identifying the
./technical/plos/journal.pbio.0020348.txt:        skeletal muscle plasticity can define the potential for adaptation in performance and
./technical/plos/journal.pbio.0020354.txt:        genus be examined, rather than a random sample of imprecisely defined close relatives, and
./technical/plos/journal.pbio.0020401.txt:        In contrast, the causes of PD are poorly defined except in those rare variant forms that
./technical/plos/journal.pbio.0020420.txt:        broadly defined, can be driven by isolation at the postzygotic level or by
./technical/plos/journal.pbio.0020431.txt:        specificity and in a well-defined fashion. This property is not common among other
./technical/plos/journal.pbio.0020431.txt:        with specificity and in well-defined structures, but the number of such pairs is limited

Usefulness: Recursively searching with grep is extremely useful for finding occurrences of a string or pattern within a complex directory structure.

Source: The recursive option is well-known, but can also be found in the grep man pages or on many Linux related websites such as GNU Grep Manual.

-i or --ignore-case: This option makes the search case-insensitive, allowing grep to match the pattern regardless of case.

Example 1:
```
grep -ri "error" ./technical/
```
This searches for the word "error" in a case-insensitive manner.

Output(cropped):

./technical/biomed/1471-2121-3-11.txt:        influenced by error of analysis. It is evident, however,
./technical/biomed/1471-2121-3-4.txt:          cytoplasm, which is within the error of the cytoplasmic
./technical/biomed/1471-213X-1-2.txt:          few migration errors. pJC15 arrays and pJC14 arrays
./technical/biomed/1471-213X-1-9.txt:          sampling error (data not shown). We, therefore, examined
./technical/biomed/1471-213X-3-7.txt:          normality of error and homogeneity of variance.
./technical/biomed/1471-2148-1-14.txt:        These sequences are preliminary and could contain errors.
./technical/biomed/1471-2148-1-4.txt:          38 ] . This two-step calibration reduced the error
./technical/biomed/1471-2148-2-15.txt:          p , but residual error variance ∈
./technical/biomed/1471-2148-2-15.txt:          Here we assume a normal distribution of errors, ∈ ~
./technical/biomed/1471-2148-2-15.txt:          payoffs plus normally distributed errors (~ N (0, 1)),
./technical/biomed/1471-2148-2-15.txt:            1 and added these as normally distributed random errors
./technical/biomed/1471-2148-2-15.txt:            variance of the normally distributed errors becomes
./technical/biomed/1471-2148-2-7.txt:        increase topological errors, and that most error is caused
./technical/biomed/1471-2148-3-1.txt:        to have a substantially lower error rate. Second, one could
./technical/biomed/1471-2148-3-1.txt:        ] . Scale-free networks are highly tolerant to error

Example 2:
```
grep -ri "warning" ./technical/
```
This command performs a case-insensitive search for "warning" within all files in the ./technical/ directory.

Output(cropped):

$ grep -ri "warning" ./technical/
./technical/911report/chapter-1.txt:    The airlines bore responsibility, too. They were facing an escalating number of conflicting and, for the most part, erroneous reports about other flights, as well as a continuing lack of vital information from the FAA about the hijacked flights. We found no evidence, however, that American Airlines sent any cockpit warnings to its aircraft on 9/11. United's first decisive action to notify its airborne aircraft to take defensive action did not come until 9:19, when a United flight dispatcher, Ed Ballinger, took the initiative to begin transmitting warnings to his 16 transcontinental flights: "Beware any cockpit intrusion- Two a/c [aircraft] hit World Trade Center." One of the flights that received the warning was United 93. Because Ballinger was still responsible for his other flights as well as Flight 175, his warning message was not transmitted to Flight 93 until 9:23.
./technical/911report/chapter-1.txt:    By all accounts, the first 46 minutes of Flight 93's cross-country trip proceeded routinely. Radio communications from the plane were normal. Heading, speed, and altitude ran according to plan. At 9:24, Ballinger's warning to United 93 was received in the cockpit. Within two minutes, at 9:26, the pilot, Jason Dahl, responded with a note of puzzlement: "Ed, confirm latest mssg plz-Jason."
./technical/911report/chapter-1.txt:    At least two callers from the flight reported that the hijackers knew that passengers were making calls but did not seem to care. It is quite possible Jarrah knew of the success of the assault on the World Trade Center. He could have learned of this from messages being sent by United Airlines to the cockpits of its transcontinental flights, including Flight 93, warning of cockpit intrusion and telling of the New York attacks. But even without them, he would certainly have understood that the attacks on the World Trade Center would already have unfolded, given Flight 93's tardy departure from Newark. If Jarrah did know that the passengers were making calls, it might not have occurred to him that they were certain to learn what had happened in New York, thereby defeating his attempts at deception.

Usefulness: The -i option is useful when the casing of the text is unknown or varied.

Source: Information about the -i option can be found in the manual pages (man grep) or on the GNU Grep Manual page.

-v or --invert-match: This inverts the search, causing grep to return lines that do not match the given pattern.

Example 1:
```
grep -rv "success" ./technical/
```
This command will print all lines from that do not contain the word "success".

Output(cropped): 

./technical/plos/pmed.0020281.txt:        D.C., on May 15th, 2005, at the invitation and support of the Public Library of Science and
./technical/plos/pmed.0020281.txt:        the Government Accountability Project feel particularly humbled and grateful to these two
./technical/plos/pmed.0020281.txt:        sponsors. Our convictions could not have been aired were it not for the essential First
./technical/plos/pmed.0020281.txt:        Amendment work of responsible journalists, who exemplify the best in investigatory
./technical/plos/pmed.0020281.txt:        research.
./technical/plos/pmed.0020281.txt:        For me, whistleblowing is not a theoretical exercise. It has a human face and tangible
./technical/plos/pmed.0020281.txt:        features. It is the face of children and adults who have been injured or killed by
./technical/plos/pmed.0020281.txt:        misrepresented pharmaceuticals; clinical research trial results that have been sequestered
./technical/plos/pmed.0020281.txt:        from the scientific community and whose incomplete findings cause injury; and
./technical/plos/pmed.0020281.txt:        pharmaceuticals that are detailed to physicians, not to save lives or necessarily improve
./technical/plos/pmed.0020281.txt:        the health or welfare of the recipients, but to make money.

Example 2:
```
grep -rv "passed" ./technical/
```
This command searches for files in ./technical/ that do not contain the word "passed".

Output(cropped):

./technical/plos/pmed.0020281.txt:        For me, whistleblowing is not a theoretical exercise. It has a human face and tangible
./technical/plos/pmed.0020281.txt:        features. It is the face of children and adults who have been injured or killed by
./technical/plos/pmed.0020281.txt:        misrepresented pharmaceuticals; clinical research trial results that have been sequestered
./technical/plos/pmed.0020281.txt:        from the scientific community and whose incomplete findings cause injury; and
./technical/plos/pmed.0020281.txt:        pharmaceuticals that are detailed to physicians, not to save lives or necessarily improve
./technical/plos/pmed.0020281.txt:        the health or welfare of the recipients, but to make money.

Usefulness: Inverting match results is useful when you want to filter out lines that contain a certain pattern.

Source: The -v option is detailed in the grep manual (man grep) and in various online resources such as GNU Grep Manual.

-l or --files-with-matches: Instead of displaying every matching line, grep will only display the names of files with lines that match the pattern.

Example 1:
```
grep -rl "failed" ./technical/
```
This command lists the names of .c files under ./technical/ that contain the word "failed".

Output(cropped):

./technical/911report/chapter-1.txt
./technical/911report/chapter-11.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-2.txt

Example 2:
```
grep -rl "function" ./technical/
```
This command lists files in the ./technical/ directory that contain the term "function".

Output:

./technical/911report/chapter-11.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-5.txt

Usefulness: This option is great for quickly identifying files that contain the pattern, without displaying the actual matching lines.

Source: The -l option is commonly used by developers and can be found in the grep manual (man grep) and on online documentation like GNU Grep Manual.
