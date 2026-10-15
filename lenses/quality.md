# Lens: quality problems

**Question:** what was wrong with the output that the human had to notice and point out? How do future agents catch it themselves?

The target notes name the **quality domain**: animation and 3D assets, form filling, code, writing, and so on. Look at that domain first, then at anything else the human rejected.

1. Collect every **correction** and **repeat correction** in `prompts.md`, and every place the human said something looked or worked wrong: "glitching", "laggy", "ugly", "not holding it correctly", "still wrong".
2. For each problem:
   - **What exactly was wrong?** Use the human's words, and the agent's own description of the fix.
   - **How long did it survive?** From first report to fixed. Did it ship anyway?
   - **Why didn't the agent catch it?** Common reasons:
     - checked in a still instead of in motion;
     - checked from one angle or view the agent picked itself;
     - no reference compared side by side;
     - "looks better" claimed without looking;
     - a fix that undid an earlier ask;
     - a performance problem never measured.
3. Turn each problem into a **check** the agent runs before it reports, plus the principle behind it. A check is something concrete: a sheet of views, a frame range in motion, a measurement, a test, or a side-by-side with the reference.
4. Add **general principles** for the domain only where they would have prevented a problem you found. For example, the classic animation principles, contact and penetration checks, or a frame-time budget.

Example from "Slop": the mic grip stayed broken for about 8 hours and shipped, a paw went through a bass, the mouth through the chin, the spine was too long, the hair had no motion, and Studio lag was never measured. The motion was checked only in still frames.
