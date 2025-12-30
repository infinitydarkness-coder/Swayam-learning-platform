# 🧪 Course XP System - Testing Guide

## Test Scenario: Complete a Course & Earn 150 XP

### Prerequisites
- Browser with console access (F12)
- Website running locally or hosted
- Clear localStorage (optional, for clean test)

---

## Step-by-Step Testing

### Step 1: Check Initial State
```javascript
// Open Console (F12)
console.log(loadLocalUserXP());
// Should show: totalXP: 0 (or current value)
```

**Expected Output:**
```
{
  totalXP: 0,
  completedCourses: [],
  hackathonRegs: [],
  xpBreakdown: { courses: 0, hackathons: 0 }
}
```

---

### Step 2: Navigate to Courses
1. Click **"🎓 Courses"** in sidebar
2. Select any course (e.g., **"Python Developer"**)
3. You should see:
   - Course title and description
   - Lesson list on sidebar
   - First lesson content displayed

---

### Step 3: Complete Lessons
1. **Read the first lesson** (or just click through)
2. Click **"Next"** button to go to next lesson
3. Continue clicking "Next" for **at least 3 lessons**
4. On the last lesson, click **"Complete Course"** button

**Tip:** You don't need to actually read everything, just navigate through lessons

---

### Step 4: Take the Quiz
When you click "Complete Course":

1. **Quiz Rules dialog appears** showing:
   - ✓ 30 random questions
   - ✓ 80% required to pass
   - ✓ Attempts remaining: 3/3
   - ✓ +150 XP for passing!

2. Click **"Start Quiz"** button

---

### Step 5: Complete the Quiz
1. For each question:
   - **Click an answer** (any option is fine for testing)
   - Click **"Next"** button
2. Continue until all 30 questions are answered
3. On the last question:
   - **Select an answer**
   - Click **"Submit"** button

---

### Step 6: Check Results

#### If Score ≥ 80% (PASS)
You'll see:
```
🎉 Congratulations!
You passed the quiz with 85%!

📄 Certificate unlocked for Python Developer

✅ +150 XP Earned!
```

✅ **This is SUCCESS!** XP should be awarded.

#### If Score < 80% (FAIL)
You'll see:
```
📚 Keep Learning
You scored 75% (Need 80% to pass)

Attempts remaining: 2
Review the material and try again!
```

🔄 **Try Again** - Click to retake the quiz

---

### Step 7: Verify XP Was Awarded
**Immediately after passing:**

1. **Look for notification** in top-right corner:
   ```
   🎉 +150 XP from Python Developer!
   ```
   - Should slide in from right
   - Show for 3 seconds
   - Slide out

2. **Check Console:**
   ```javascript
   console.log(localStorage.getItem('user_total_xp'));
   // Should show: "150"
   
   console.log(loadLocalUserXP());
   // Should show: totalXP: 150, courses: 150
   ```

3. **Check localStorage keys:**
   ```javascript
   localStorage.getItem('user_Python Developer_completed');
   // Should show: "true"
   
   JSON.parse(localStorage.getItem('user_completed_courses'));
   // Should show: [{course: "Python Developer", xp: 150, date: "..."}]
   ```

---

### Step 8: Check Dashboard

1. **Navigate to Dashboard** (🏠 button in sidebar)
2. **Look at "Your Progress" card:**
   ```
   ┌─────────────┐
   │  150 XP     │  ← Should show your earned XP
   └─────────────┘
   ```

3. **Look at "Daily Quests":**
   ```
   ✓ Courses Completed (1) - 150 XP
   ✓ Hackathons Registered (0) - 0 XP
   ```

4. **Progress ring** should be filled to 30% (150/500)

---

## ✅ Test Checklist

**Before Quiz:**
- [ ] Navigated to Courses
- [ ] Selected a course
- [ ] Clicked through at least 3 lessons
- [ ] Initial XP was 0

**During Quiz:**
- [ ] Quiz rules dialog appeared
- [ ] Quiz started with questions
- [ ] Was able to answer all questions
- [ ] Submit button appeared on last question

**After Quiz:**
- [ ] Saw pass/fail result
  - [ ] If passed (≥80%): Saw success screen
  - [ ] If failed (<80%): Saw retry screen

**XP Verification:**
- [ ] Notification appeared: "🎉 +150 XP from [Course]!"
- [ ] localStorage.getItem('user_total_xp') = "150"
- [ ] loadLocalUserXP() shows totalXP: 150
- [ ] user_${course}_completed flag is set

**Dashboard:**
- [ ] Dashboard shows 150 XP in progress ring
- [ ] Daily Quests shows "Courses Completed (1) - 150 XP"
- [ ] Progress ring filled to ~30%

---

## 🐛 Troubleshooting

### Issue: Quiz won't start
**Solution:** 
- Refresh the page
- Make sure JavaScript is enabled
- Check console for errors (F12)

### Issue: Quiz passes but no notification
**Solution:**
- Check if you're looking in the right corner (top-right)
- Check browser console for JS errors
- Verify notification CSS is loaded

### Issue: XP not showing in localStorage
**Solution:**
- Open console and check: `localStorage.getItem('user_total_xp')`
- If empty, XP wasn't awarded - check quiz results
- Try refreshing dashboard

### Issue: XP showing in console but not on dashboard
**Solution:**
- Close and reopen dashboard
- Clear browser cache (Ctrl+Shift+Delete)
- Verify dashboard is loading the XP function

---

## 📊 Success Criteria

✅ **Test Passes If:**
1. User completes course lessons
2. Quiz appears with correct rules
3. User passes quiz (≥80%)
4. XP notification appears (🎉)
5. localStorage updated with +150 XP
6. Dashboard displays updated XP
7. Daily Quests shows course in list

❌ **Test Fails If:**
- Any step doesn't complete
- XP not added to localStorage
- Dashboard doesn't update
- Duplicate XP awarded on retry

---

## 🔄 Full Test Scenarios

### Scenario 1: Single Course Completion
1. Complete Python Developer course
2. Pass quiz
3. ✅ Should have 150 XP
4. ✅ Progress ring at 30%

### Scenario 2: Multiple Course Completions
1. Complete Python Developer → +150 XP
2. Complete HTML course → +150 XP
3. ✅ Should have 300 XP total
4. ✅ Progress ring at 60%
5. ✅ Daily Quests shows both courses

### Scenario 3: Failed Quiz & Retry
1. Complete course
2. Take quiz
3. Fail (< 80%)
4. ✅ Retry button appears
5. Retry quiz
6. Pass (≥ 80%)
7. ✅ Only get 150 XP once (not twice)

### Scenario 4: Course Completion Without Quiz
1. Complete course without quiz
2. ✅ No XP awarded yet
3. Click "Complete Course" again
4. Take quiz and pass
5. ✅ Get 150 XP

---

## 📸 Expected Screenshots

### Quiz Rules Screen
```
┌─────────────────────────────────────────┐
│  🎯 Python Developer Quiz Challenge      │
│                                          │
│  📋 Quiz Rules & Information             │
│  ┌────────────────────────────────────┐  │
│  │ Total Questions: 30                │  │
│  │ Total Marks: 30                    │  │
│  │ Passing Score: 80%                 │  │
│  │ Attempts Left: 3/3                 │  │
│  │                                    │  │
│  │ ⚠️ Important Rules:                 │  │
│  │ • Must score at least 80% to pass  │  │
│  │ • 3 total attempts                 │  │
│  │ • Questions randomly selected      │  │
│  │ • Answer all before submitting     │  │
│  │                                    │  │
│  │ [Cancel]         [Start Quiz]      │  │
│  └────────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

### Pass Screen
```
┌─────────────────────────────────────────┐
│  🎉 Congratulations!                     │
│                                          │
│  You passed the quiz with 85%!           │
│  📄 Certificate unlocked for Python Dev  │
│                                          │
│  ┌────────────────────────────────────┐  │
│  │  +150 XP Earned!                   │  │
│  └────────────────────────────────────┘  │
│                                          │
│          [Continue]                      │
└─────────────────────────────────────────┘
```

### XP Notification
```
┌──────────────────────────────┐
│ 🎉 +150 XP from Python Dev!  │
└──────────────────────────────┘
(Top-right corner, 3 seconds)
```

### Dashboard Update
```
┌─────────────────────┐
│  🎯 Your Progress   │
│  ┌───────────────┐  │
│  │   150 XP      │  │
│  └───────────────┘  │
│  🔥 Streak: 0 days  │
│                     │
│  🎯 Daily Quests    │
│  ☑ Courses Completed(1)
│     - 150 XP        │
│  ☑ Hackathons Reg(0)│
│     - 0 XP          │
└─────────────────────┘
```

---

## 🎯 Next Steps After Testing

**If Test PASSED:**
- ✅ Move to testing Hackathon XP
- ✅ Test multiple course completions
- ✅ Test dashboard updates
- ✅ Test on mobile devices

**If Test FAILED:**
1. Check console for errors (F12)
2. Review implementation files
3. Verify all code changes were applied
4. Test in different browser
5. Check localStorage is enabled

---

## 💻 Debug Commands

```javascript
// Check current XP
localStorage.getItem('user_total_xp');

// Load all XP data
loadLocalUserXP();

// Check course completion flag
localStorage.getItem('user_Python Developer_completed');

// View all courses completed
JSON.parse(localStorage.getItem('user_completed_courses'));

// Clear and reset (WARNING: removes all data!)
localStorage.clear();

// Set test data
localStorage.setItem('user_total_xp', '150');
localStorage.setItem('user_Python Developer_completed', 'true');
```

---

## 📞 Support

**If something goes wrong:**
1. Check browser console for error messages
2. Verify all code modifications were applied
3. Check that localStorage is enabled
4. Try clearing cache and reloading
5. Test in incognito/private mode

---

**Test Date**: December 20, 2025  
**Status**: Ready for Testing  
**Expected Result**: ✅ 150 XP awarded on course completion
