Question 17: Show the start and end date in the date picker. But the end date should be 29 days ago from the start date. What will be your approach to getting this problem statement?

source code:import 'package:flutter/material.dart';
import 'package:intl/intl.dart'; // for formatting dates

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: DatePickerScreen(),
    );
  }
}

class DatePickerScreen extends StatefulWidget {
  @override
  _DatePickerScreenState createState() => _DatePickerScreenState();
}

class _DatePickerScreenState extends State<DatePickerScreen> {
  DateTime? startDate;
  DateTime? endDate;

  // Function to pick start date
  Future<void> pickStartDate(BuildContext context) async {
    DateTime now = DateTime.now();
    final DateTime? picked = await showDatePicker(
      context: context,
      initialDate: now,
      firstDate: DateTime(2000),
      lastDate: now,
    );

    if (picked != null) {
      setState(() {
        startDate = picked;
        // End date is 29 days before the start date
        endDate = startDate!.subtract(Duration(days: 29));
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    String startDateText =
        startDate != null ? DateFormat('yyyy-MM-dd').format(startDate!) : 'Select Start Date';
    String endDateText =
        endDate != null ? DateFormat('yyyy-MM-dd').format(endDate!) : 'End Date';

    return Scaffold(
      appBar: AppBar(title: Text('Date Picker Example')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () => pickStartDate(context),
              child: Text(startDateText),
            ),
            SizedBox(height: 20),
            Text(
              endDateText,
              style: TextStyle(fontSize: 18),
            ),
          ],
        ),
      ),
    );
  }
}


Hint 1:- Use the date picker library for selecting the start and end date.

Hint 2:- Add the logic which is end data should be 29 days ago from the start date.
