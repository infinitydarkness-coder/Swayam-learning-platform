# 🎮 Swayam XP System Documentation

## Overview
The XP system connects experience points from courses, hackathons, and quizzes to a persistent user account on the dashboard. All XP data is stored in localStorage and displayed in real-time on the dashboard.

---

## 🏆 XP Rewards

### From Courses
- **Course Completion Quiz Pass**: +150 XP
  - Awarded when user completes a course and passes the final quiz (80% score)
  - Stored in: `user_${courseKey}_completed`
  - Cannot be earned twice per course

### From Hackathons
- **Hackathon Registration**: +100 XP
  - Awarded immediately when user clicks "Register" button
  - Stored separately in: `user_hackathon_registrations`

### Total XP Storage
All XP is accumulated in: `user_total_xp` (localStorage)

---

## 📊 Data Structure

### LocalStorage Keys

#### 1. **user_total_xp**
```
Key: 'user_total_xp'
Value: Integer (e.g., 350)
Description: Total XP earned from all sources
```

#### 2. **user_completed_courses**
```
Key: 'user_completed_courses'
Value: Array of objects
[
  {
    course: "Python Developer",
    xp: 150,
    date: "2025-12-20T10:30:00.000Z"
  },
  ...
]
```

#### 3. **user_hackathon_registrations**
```
Key: 'user_hackathon_registrations'
Value: Array of objects
[
  {
    hackathon: "Hackathon Name",
    xp: 100,
    date: "2025-12-20T10:30:00.000Z"
  },
  ...
]
```

#### 4. **user_${courseKey}_completed**
```
Key: 'user_Python Developer_completed'
Value: 'true'
Description: Prevents duplicate XP awards for same course
```

---

## 🎯 How It Works

### Course Completion Flow
1. User completes all lessons in a course
2. Clicks "Complete Course" button
3. Takes the course quiz
4. **Passes (≥80%)** → `awardCourseXP()` is called
5. Function:
   - Adds 150 XP to `user_total_xp`
   - Records completion in `user_completed_courses`
   - Sets `user_${courseKey}_completed` flag
   - Shows XP notification popup

### Hackathon Registration Flow
1. User clicks "Register" button on hackathon card
2. `registerHackathon()` function is called
3. Function:
   - Adds hackathon to `myHackathons` list
   - Calls `awardHackathonXP()`
4. `awardHackathonXP()` function:
   - Adds 100 XP to `user_total_xp`
   - Records in `user_hackathon_registrations`
   - Shows XP notification popup

### Dashboard Display Flow
1. Page loads and calls `loadLocalUserXP()`
2. Function aggregates data from:
   - `user_total_xp` (main total)
   - `user_completed_courses` (course breakdown)
   - `user_hackathon_registrations` (hackathon breakdown)
3. Displays total XP in progress ring (max 500 XP shown)
4. Shows XP sources in "Daily Quests" section:
   - Courses Completed (X) - Y XP
   - Hackathons Registered (X) - Y XP
5. Updates in real-time as user completes courses/hackathons

---

## 🔔 XP Notifications

When user earns XP, a notification appears:

```
🎉 +150 XP from Python Developer!
```

Or for hackathons:

```
🎉 +100 XP from Hackathon Registration!
```

**Features:**
- Appears in top-right corner
- Duration: 3 seconds
- Slide-in animation from right
- Slide-out animation to fade away
- Uses gradient background (purple/blue)

---

## 📈 Dashboard Integration

### XP Progress Ring
- Shows total XP earned
- Max capacity: 500 XP
- Circular progress indicator
- Centered text: "XXX XP"

### Daily Quests Section
- Displays auto-tracked quests:
  - ✓ Courses Completed (N) - M XP
  - ✓ Hackathons Registered (N) - M XP
- Quests are marked complete if user has earned XP from them

### Analytics Charts
- XP Growth: Line chart showing XP progression
- Activity Pie Chart: Distribution of XP sources
  - Courses
  - Quizzes
  - Hackathons

---

## 🔐 Data Persistence

### LocalStorage (Client-Side)
- XP data persists across browser sessions
- Works offline (data not synced with backend)
- Located in browser's localStorage

### Supabase Integration (Optional)
- Dashboard also uses Supabase for user profiles
- Can sync XP to database later for:
  - Leaderboards
  - Server-side verification
  - Data backup

---

## 📱 Mobile Friendly

All features work on mobile:
- XP notifications adapt to screen size
- Progress ring is responsive
- Touch-friendly buttons

---

## 🧪 Testing the System

### Test Course Completion
1. Go to **Courses** page
2. Select any course (e.g., "Python Developer")
3. Complete all lessons
4. Click "Complete Course"
5. Take quiz and score ≥80%
6. Should see: "🎉 +150 XP" notification
7. Check dashboard → XP ring should increase

### Test Hackathon Registration
1. Go to **Hackathons** page
2. Click "Register" on any hackathon
3. Should see: "✅ Registered + 🎉 +100 XP earned!"
4. Check dashboard → XP ring should increase

### Debug Info
Open browser console (F12) and check:
```javascript
// View all XP data
console.log({
  total: localStorage.getItem('user_total_xp'),
  courses: JSON.parse(localStorage.getItem('user_completed_courses')),
  hackathons: JSON.parse(localStorage.getItem('user_hackathon_registrations'))
})
```

---

## 🛠️ Files Modified

1. **course-details.html**
   - Added `awardCourseXP()` function
   - Added `showXPNotification()` function
   - Integrated into quiz submission flow
   - Added CSS animations

2. **hackathons.html**
   - Updated `registerHackathon()` function
   - Added `awardHackathonXP()` function
   - Added `showXPNotification()` function
   - Added CSS animations

3. **dashboard.html**
   - Added `loadLocalUserXP()` function
   - Updated `setXpUI()` to support 500 XP max
   - Updated `renderQuests()` to show course/hackathon XP
   - Integrated local XP with profile data
   - Real-time sync with localStorage

---

## 🚀 Future Enhancements

### Planned Features
- [ ] Leaderboard system using total XP
- [ ] Achievements/badges for XP milestones
- [ ] Daily login streaks
- [ ] XP decay system
- [ ] Levels based on total XP
- [ ] Team-based XP challenges
- [ ] Seasonal XP resets
- [ ] Admin dashboard to manage XP values

### Database Sync
- [ ] Sync XP to Supabase on course completion
- [ ] Server-side XP verification
- [ ] Prevent XP farming/cheating
- [ ] Backup user progress

---

## 💡 FAQ

**Q: Can users earn XP multiple times for same course?**
A: No. XP is awarded only once per course. Subsequent completions don't grant XP.

**Q: What if user clears browser data?**
A: XP data will be lost. Data is only stored locally in browser localStorage.

**Q: How to reset user XP?**
A: Open console and run:
```javascript
localStorage.removeItem('user_total_xp');
localStorage.removeItem('user_completed_courses');
localStorage.removeItem('user_hackathon_registrations');
// Remove course completion flags
Object.keys(localStorage).forEach(key => {
  if (key.includes('_completed')) localStorage.removeItem(key);
});
```

**Q: Why is max XP 500 in ring?**
A: The progress ring is designed to show progress within a session. Can be increased by changing:
```javascript
const max = 500; // Change this value in setXpUI()
```

---

## 📞 Support

For issues or questions about the XP system:
1. Check browser console (F12) for errors
2. Verify localStorage has correct keys
3. Ensure JavaScript animations are enabled
4. Clear cache and reload page

---

**Version:** 1.0  
**Last Updated:** December 20, 2025  
**Status:** ✅ Active & Functional
