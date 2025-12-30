# 🧪 Course XP Testing - Quick Checklist

## Phase 1: Setup ✓
```
[ ] Open your Swayam platform
[ ] Open Browser Console (F12)
[ ] Note initial XP: 
    console.log(loadLocalUserXP())
    Current: ________________
```

---

## Phase 2: Course Selection & Lessons ✓
```
[ ] Click "🎓 Courses" in sidebar
[ ] Select a course (e.g., Python Developer)
[ ] Verify course loaded
    - Title visible: ________________
    - Lessons showing in sidebar
[ ] Click "Next" to go through lessons
[ ] Complete at least 3 lessons
```

---

## Phase 3: Quiz Start ✓
```
[ ] Click "Complete Course" button
[ ] Quiz Rules dialog appears
[ ] Verify shown:
    - Questions: 30
    - Passing Score: 80%
    - Attempts: 3/3
    - XP Reward: 150 XP
[ ] Click "Start Quiz"
```

---

## Phase 4: Quiz Completion ✓
```
[ ] Answer all 30 questions
    - Total answered: 30/30
    - Progress: 100%
[ ] Click "Submit" on final question
```

---

## Phase 5: Results ✓
```
[ ] Check quiz result:
    ○ PASS (≥80%) ✓ Continue to Phase 6
    ○ FAIL (<80%) → Retake and pass, then continue
    
[ ] Score: _____%
```

---

## Phase 6: XP Award ✓
```
[ ] NOTIFICATION CHECK
    [ ] See "🎉 +150 XP" notification
    [ ] Top-right corner
    [ ] Duration: ~3 seconds
    [ ] Animation: Slide-in/out
    
[ ] CONSOLE CHECK
    console.log(localStorage.getItem('user_total_xp'));
    Expected: "150"
    Actual: ________________
    
[ ] COMPLETION FLAG
    console.log(localStorage.getItem('user_Python Developer_completed'));
    Expected: "true"
    Actual: ________________
    
[ ] HISTORY LOG
    console.log(JSON.parse(localStorage.getItem('user_completed_courses')));
    Expected: [{course: "Python Developer", xp: 150, date: "..."}]
    Actual: ________________
```

---

## Phase 7: Dashboard Verification ✓
```
[ ] Close quiz modal
[ ] Navigate to Dashboard (🏠)
[ ] Check Progress Ring:
    [ ] Shows "150 XP"
    [ ] Ring filled to ~30%
    [ ] Color: Blue
    
[ ] Check Daily Quests:
    [ ] Shows "Courses Completed (1)"
    [ ] Shows "150 XP"
    [ ] Checkbox marked
    
[ ] Check Analytics:
    [ ] XP Growth chart visible
    [ ] Activity pie chart visible
```

---

## ✅ Final Verification

```
XP System Status:
├─ Notification Shown: [ ] YES  [ ] NO
├─ localStorage Updated: [ ] YES  [ ] NO  
├─ Dashboard Displays XP: [ ] YES  [ ] NO
├─ Completion Flag Set: [ ] YES  [ ] NO
└─ Data Persists (reload): [ ] YES  [ ] NO
```

---

## 🎯 Success = All Checks Passed ✓

If ALL checked, Course XP System is WORKING! 🎉

---

## 📝 Notes

```
Additional observations:
_________________________________________________
_________________________________________________
_________________________________________________
```

---

## 🐛 Issues Found

```
[ ] None - All working!

[ ] Issues:
_________________________________________________
_________________________________________________
```

---

## Next Test

After passing Course XP test:
- [ ] Test Hackathon XP system
- [ ] Test multiple courses
- [ ] Test on mobile
- [ ] Test browser compatibility

---

**Date**: _________  
**Browser**: _________  
**Status**: ✅ PASSED / ❌ FAILED
