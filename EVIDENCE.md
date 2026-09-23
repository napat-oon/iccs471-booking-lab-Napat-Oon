# Booking Lab Evidence Record

**Name:** Napat Oonsamatham
**Student ID:** 6680964
**Repository:** https://github.com/napat-oon/iccs471-booking-lab-Napat-Oon

## Goal
I was asked to make changes only in 'booking_app\booking.py' and 'tests\test_booking.py' without touching the original code there. All tests pass, but 'demo.py' shows that there is an unacceptable, overlapping booking so the overlapping detection is needed and new tests are to be created for overlapping booking behavior.

## Constraints / Out of Scope
Only 'booking_app\booking.py' and 'tests\test_booking.py' are allowed to be changed, while retaining all original behaviors. 'demo.py' and other files are NOT allowed (remain intact). 

## Key Decision and Agent Claim
The entire Planning part is the most deliberately checked and accepted because if I missed any mistake made by Copilot such as accidentally changing other files that are not assigned, or making unallowed changes to the original code, I would have to undo or fallback to when before the changes happened. That could disrupt the flow of both me and Copilot. In some case, AI may suggest an entirely different approach when asked to plan/suggest again (with the same prompt). (I have had this experience before on other assignments, but I have not known if this issue still exists).

I made no correction in the planning process because I read through Copilot's plan thoroughly to make sure it understood the prompt and (especially) the constraints correctly. Only pressing "Start Implementation" if I consciously understood what Copilot was going to do (which was updating 'booking_app\booking.py' and extending 'tests\test_booking.py' inside the limited scope). (Copilot did suggest verification with 'python -m unittest tests.test_booking' or 'python -m pytest -q' if pytest is installed in Plan mode, and it asked me to manually approve the command in Agent mode, but I declined it since we were using 'uv' to execute the tests). 

After the implementation is finished, Copilot claimed that it applied the overlap rule and expanded the tests in two permitted files. I still checked two files again, even after verifying the plan myself, to make sure the changes are applied correctly as I expected. I manually approved all code changes and confirmed that the overlap rule indeed returned 'ValueError' and rejected the booking into the list (inside 'booking_app\booking.py'), while adjacent bookings and different-room overlaps remain valid (using new tests inside 'tests\test_booking.py'). 

## Verification: Claim → Evidence
- **Claim:** I want to establish that the new overlap rule is correctly working, with the current tests and new ones revolving around the rule.
- **Command or test I ran:** 'uv run python -m unittest discover -s tests -v' (after adding and confirming new tests) and 'uv run python demo.py'
- **Actual result:** All test cases return OK, and 'demo.py' rejected the overlapping booking along with error message (and the number of bookings is 3).
- **What this supports:** This makes me believe that the implementation does not interfere with old tests and convinces me that new tests pass as intended, along with the correctly rejected booking in 'demo.py'.

## Manual Validation
It shows that the bookings are accepted correctly for adjacent times and different rooms on the overlapping time, and rejected the booking that would overlap with the existing booking(s) for the same room.

## Remaining Uncertainty
One possible booking case that my checks did not fully establish is booking in later times before booking in earlier times such as 1st booking in Room A, 10:00-11:00, THEN 2nd booking in Room A, 09:00-10:00.