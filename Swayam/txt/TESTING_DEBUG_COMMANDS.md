# 🔧 Console Debug Commands for Course XP Testing

## Quick Commands to Copy-Paste

### 1️⃣ Check All XP Data
```javascript
loadLocalUserXP()
```
**What it shows**: Total XP, courses completed, hackathons registered, XP breakdown

**Expected Output** (after passing course):
```javascript
{
  totalXP: 150,
  completedCourses: [
    {course: "Python Developer", xp: 150, date: "2025-12-20T..."}
  ],
  hackathonRegs: [],
  xpBreakdown: {courses: 150, hackathons: 0}
}
```

---

### 2️⃣ Check Total XP Only
```javascript
localStorage.getItem('user_total_xp')
```
**What it shows**: Just the total XP number

**Expected**: `"150"` (as a string)

---

### 3️⃣ Check Completed Courses
```javascript
JSON.parse(localStorage.getItem('user_completed_courses'))
```
**What it shows**: List of all courses completed with XP and date

**Expected**:
```javascript
[
  {
    course: "Python Developer",
    xp: 150,
    date: "2025-12-20T15:30:00.000Z"
  }
]
```

---

### 4️⃣ Check Course Completion Flag
```javascript
localStorage.getItem('user_Python Developer_completed')
```
**What it shows**: Whether course was already completed

**Expected**: `"true"`

---

### 5️⃣ Check All LocalStorage
```javascript
{
  totalXP: localStorage.getItem('user_total_xp'),
  courses: JSON.parse(localStorage.getItem('user_completed_courses')),
  hackathons: JSON.parse(localStorage.getItem('user_hackathon_registrations')),
  pythonFlag: localStorage.getItem('user_Python Developer_completed'),
  htmlFlag: localStorage.getItem('user_HTML_completed')
}
```
**What it shows**: Everything at once in a nice object

---

### 6️⃣ View All LocalStorage Keys
```javascript
Object.keys(localStorage)
```
**What it shows**: All keys stored in browser

**Expected** (includes):
```javascript
[
  "user_total_xp",
  "user_completed_courses",
  "user_Python Developer_completed",
  ...
]
```

---

## ✅ Test Scenarios with Commands

### Scenario 1: After Completing First Course

**Run this sequence:**
```javascript
// 1. Check if anything stored yet
loadLocalUserXP()

// 2. Complete course and pass quiz, then run:
localStorage.getItem('user_total_xp')
// Should be: "150"

// 3. Check course list
JSON.parse(localStorage.getItem('user_completed_courses'))
// Should show 1 course with 150 XP

// 4. Check dashboard loaded XP
console.log(loadLocalUserXP())
// totalXP should be 150
```

---

### Scenario 2: After Completing Second Course

**Run this sequence:**
```javascript
// 1. Before second course
loadLocalUserXP()
// totalXP should be 150

// 2. Complete second course and pass quiz, then run:
localStorage.getItem('user_total_xp')
// Should be: "300"

// 3. Check both courses listed
JSON.parse(localStorage.getItem('user_completed_courses'))
// Should show 2 courses with 300 XP total

// 4. Verify breakdown
loadLocalUserXP()
// totalXP should be 300
// xpBreakdown.courses should be 300
```

---

### Scenario 3: Verify No Duplicate XP

**Run this sequence:**
```javascript
// 1. Check initial state
console.log(loadLocalUserXP().totalXP)
// Should be: 300

// 2. Go back to same course
// Complete it again and pass quiz

// 3. Check if XP increased
console.log(localStorage.getItem('user_total_xp'))
// Should STILL be: "300" (not 450!)

// 4. Verify course only listed once
console.log(JSON.parse(localStorage.getItem('user_completed_courses')).length)
// Should be: 2 (two different courses, not 3)
```

---

## 🧹 Data Management Commands

### Clear All XP Data (RESET)
```javascript
localStorage.clear()
location.reload()
```
⚠️ **WARNING**: Removes ALL data from browser storage!

---

### Clear Specific Key
```javascript
localStorage.removeItem('user_total_xp')
localStorage.removeItem('user_completed_courses')
localStorage.removeItem('user_Python Developer_completed')
location.reload()
```

---

### Set Test Data (Manual)
```javascript
// Set total XP to 250
localStorage.setItem('user_total_xp', '250')

// Set completed courses
localStorage.setItem('user_completed_courses', JSON.stringify([
  {course: "Python Developer", xp: 150, date: new Date().toISOString()},
  {course: "HTML", xp: 100, date: new Date().toISOString()}
]))

// Set completion flag
localStorage.setItem('user_Python Developer_completed', 'true')

// Reload to see changes
location.reload()
```

---

## 🔍 Debugging Commands

### Check if Function Exists
```javascript
typeof loadLocalUserXP === 'function'
// Should return: true
```

---

### Check if awardCourseXP Exists
```javascript
typeof awardCourseXP === 'function'
// Should return: true
```

---

### Monitor Console Logs
```javascript
// During quiz completion, watch for:
// "✅ Awarded 150 XP for completing Python Developer"
// This shows in console if award function ran
```

---

### Check Browser LocalStorage Limit
```javascript
// Show how much storage is used
(() => {
  let total = 0;
  for(let key in localStorage) {
    if(localStorage.hasOwnProperty(key)) {
      total += localStorage[key].length + key.length;
    }
  }
  console.log('Storage used: ' + (total / 1024).toFixed(2) + ' KB');
})()
```

---

## 📊 Comparison Tests

### Before Quiz
```javascript
loadLocalUserXP()
```
Example:
```
{totalXP: 0, completedCourses: [], ...}
```

---

### After Passing Quiz
```javascript
loadLocalUserXP()
```
Expected:
```
{totalXP: 150, completedCourses: [...], ...}
```

**Difference**: totalXP increased by 150 ✓

---

## 🎯 What Each Part Means

| Command | Shows | Location |
|---------|-------|----------|
| `loadLocalUserXP()` | Complete XP summary | Dashboard |
| `localStorage.getItem('user_total_xp')` | Raw XP number | Storage |
| `JSON.parse(...)` | Course history | Storage |
| `localStorage.getItem('user_[COURSE]_completed')` | Completion flag | Storage |

---

## 💡 Pro Tips

1. **Copy full command** and paste into console
2. **Press Enter** to execute
3. **Check output** in console
4. **Compare** with expected values
5. **Screenshot** if something wrong

---

## 🚨 Common Errors & Fixes

### "loadLocalUserXP is not defined"
- Function not loaded
- Refresh the page
- Check you're on the right page

### "localStorage.getItem(...) returns null"
- Data not saved
- Quiz wasn't completed successfully
- Try completing course again

### Shows 0 XP after quiz pass
- Check if quiz result was "PASS"
- Check browser console for error messages
- Verify notification appeared

---

## 📱 Mobile Console Testing

**On Mobile:**
1. Long-press on page
2. Select "Inspect" (if available)
3. Go to "Console" tab
4. Paste commands above
5. Check outputs

**Or use Chrome DevTools via USB:**
1. Connect phone via USB
2. Open Chrome DevTools on desktop
3. Select phone device
4. Run same commands

---

## 📝 Testing Log Template

```javascript
// Copy and update after each test:

// TEST 1: Complete Python Course
const test1Before = localStorage.getItem('user_total_xp');
// Completed course and quiz...
const test1After = localStorage.getItem('user_total_xp');
console.log(`Test 1: ${test1Before} → ${test1After}`);
// Expected: "0" → "150"

// TEST 2: Complete HTML Course
const test2Before = localStorage.getItem('user_total_xp');
// Completed course and quiz...
const test2After = localStorage.getItem('user_total_xp');
console.log(`Test 2: ${test2Before} → ${test2After}`);
// Expected: "150" → "300"
```

---

## 🎯 Success Indicators

✅ **If these are true, Course XP is working:**
```javascript
loadLocalUserXP().totalXP > 0
localStorage.getItem('user_total_xp') === '150'
loadLocalUserXP().completedCourses.length > 0
loadLocalUserXP().xpBreakdown.courses === 150
```

❌ **If these are false, something's wrong:**
```javascript
loadLocalUserXP().totalXP === 0
localStorage.getItem('user_total_xp') === null
loadLocalUserXP().completedCourses.length === 0
```

---

## 🔗 Related Testing

- Course XP Testing: `TESTING_COURSE_XP.md`
- Hackathon XP Testing: `TESTING_HACKATHON_XP.md` (coming)
- Full Documentation: `XP_SYSTEM_README.md`

---

**Ready to test!** Copy commands above and try them out! 🚀
