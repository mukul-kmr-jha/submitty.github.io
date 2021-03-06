---
title: iClicker Configuration
category: Instructor
order: 12
---


## Collecting iClicker IDs by Submitty Gradeable

You can bypass the iclicker.com registration site and software by
directly collecting remote IDs from the students via Submitty.

If you've collected iclicker IDs using the
[iclicker gradeable configuration](https://github.com/Submitty/Submitty/tree/master/more_autograding_examples/iclicker_upload/config),
you can scrape the iclicker with this command:

```
/usr/local/submitty/bin/read_iclicker_ids.py /var/local/submitty/courses/<SEMESTER>/<COURSE>/submissions/<ICLICKER GRADEABLE>/ <INSERT REMOTE ID DESTINATION FILE>
```

Note: Students often misunderstand which digits on the back of their
remote are their unique remote ID.  Many type in the model number of
the clicker that begins with "T24" or something.  The remote ID is the
8 digit number/letter string that is on the white sticker next to the
battery.


## Remote ID file

Your iClicker remote id file should be a simple CSV file mapping
iClicker IDs to student IDs, an example row might read:

```
#123ABC,"smithj"
```

The leading ``#``, the letters in the iClicker ID being capitalized, and
the student ID being wrapped in quotation marks are all important.

NOTE: iClicker support is based on iClicker software version 6, and may not
work with newer versions.



## Remote ID file

In `customization.json` there are only two additional entries needed to
make iClickers work.

* **field:** ``"iclicker_ids"``  
  **type:** _string_  
  **REQUIRED** for iClickers

  The string is a relative path (it can just be a name if it is in the
  `grades_summary` directory).

* **field:** ``"iclicker"``  
  **type:** _associative array of string to array_  
  **REQUIRED** for iClickers

  This array maps lecture numbers (e.g. ``"2"`` for lecture 2) to an array
  of associative arrays, where each of the inner associative arrays corresponds
  to one iClicker question.

  The inner array format is:

  * **field:** ``"file"``  
    **type:** _array_  
    **REQUIRED**

    An array of strings, where each string is a relative path to a iClicker session file 
   (should look something like LYYMMDDHHII.csv or .xml, where YY is the 2-digit year 00-99, 
    MM is the 2-digit month 01-12, DD is the 2-digit day 01-31, HH is the two digit hour 00-23, 
    and II is the 2-digit minute 00-59). Multiple files can be used for one lecture. Currently,
    multiple files can be used for one question even, but the column number and correct answer(s)
    must match in the files.

  * **field:** ``"column"``  
    **type:** _integer_  
    **REQUIRED**

    This field specifies which question in the iClicker session to read student responses from.
    Each question is one column, so to get the third question you would use ``"column": 3``.

  * **field:** ``"answer"``  
    **type:** _string_  
    **REQUIRED**

    The correct answer(s) should be in this string. Multiple answers can be counted as correct,
    simply use multiple letters with no spaces. If all five letters are used (``"answer": "ABCDE"``),
    the question is considered a poll question and Rainbow Grades will highlight student responses in
    yellow. For any other question, student responses will be highlighted in green if they are correct
    (1.0 points towards iClicker score) and red if they are incorrect (0.5 points towards iClicker score).


Below is a short example which gets questions 2.1 (a poll) and 2.2 (two right answers) from one file,
and 2.3 from another file which also contains 3.1 (a poll).


```     
"iclicker_ids": "clicker_data/RemoteID.csv",
"iclicker": {
  "2": [
    {"file": "clicker_data/L1701201013.csv", "column": 1, "answer": "ABCDE"},
    {"file": "clicker_data/L1701201013.csv", "column": 2, "answer": "AE"},
    {"file": "clicker_data/L1701220958.csv", "column": 1, "answer": "D"},
  ],     
  "3": [
    {"file": "clicker_data/L1701220958.csv", "column": 2, "answer": "ABCDE"},           
  ]
}
```

