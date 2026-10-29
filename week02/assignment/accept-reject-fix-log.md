# Week 2 · Accept / reject / fix log

**Name:** <Mariia Parkhomchuk>
**Date:** <28-10-2026>

## Issue
- **Issue claimed:** #2, `top_students` returns one student too few
- **What the fix should change:** Make `top_students` return the requested number of ranked `(name, average)` pairs, or all graded students when fewer are available.
- **Existing test that confirms it:** `tests/test_reports.py::test_top_students_returns_the_requested_number_in_rank_order`
- **Branch:** Not created yet — GitHub repository access and repository setup are pending.

---

## Log entries (one per agent action)

### Action 1
- **Agent action:** In a previous chat, I asked ChatGPT to help fix the off-by-one error in top_students(). The return slice was changed from pairs[:count - 1] to pairs[:count].
- **Files changed:** week02/assignment/mini-project/gradebook/reports.py
- **Your explanation (teach-back):** Python slicing excludes the ending index. Using pairs[:count - 1] returns at most count - 1 elements. Using pairs[:count] returns up to count elements. If fewer students are available, slicing returns all available students.
- **Evidence / test result:** uv run --with pytest pytest -q -k test_top_students_returns_the_requested_number_in_rank_order — 1 passed, 20 deselected.
- **Decision:** accept 
- **Follow-up prompt:** Asked ChatGPT to help verify the fix and understand the test results.

### Action 2
- **Agent action:**ChatGPT helped inspect the full test suite and identify the remaining failures.
- **Files changed:** None.
- **Your explanation (teach-back):** The full test suite reported two unrelated failures: whitespace-only names are accepted, and calculating the average for a student with no scores raises ZeroDivisionError. These correspond to Issues 1 and 3, which were not changed.
- **Evidence / test result:** uv run --with pytest pytest -q — 2 failed, 19 passed. The failing tests were test_averages_handle_students_with_no_recorded_scores and test_add_student_rejects_whitespace_only_name.
- **Decision:** accept 
- **Follow-up prompt:** Asked ChatGPT to help inspect the original ZIP archive to compare the starter version with the working copy.

### Action 3
- **Agent action:** ChatGPT helped inspect the original ZIP archive using PowerShell's tar command and compare its reports.py with the working copy.
- **Files changed:** None during this inspection.
- **Your explanation (teach-back):** The original ZIP contains return pairs[:count - 1], while the working copy contains return pairs[:count]. This confirms that the working copy has the Issue 2 fix, although it has not yet been verified through the required Agent Mode workflow.
- **Evidence / test result:** The original file was printed with tar -xOf. The working copy's targeted test passed.
- **Decision:** accept 
- **Follow-up prompt:** None.

### Action 4
- **Agent action:** Used ChatGPT to help create a Git branch, prepare the assignment files, exclude Python cache files, and push the branch to the personal GitHub repository.
- **Files changed:** Added .gitignore; committed the assignment files, including the corrected reports.py and this log.
- **Your explanation (teach-back):** A separate branch keeps the proposed change isolated from main. The .gitignore excludes Python bytecode and test caches so they do not clutter the submission. The branch was pushed to the personal repository because access to the course repository was unavailable.
- **Evidence / test result:** Commit 0dede2a was created, and git push -u origin week02-issue2 completed successfully.
- **Decision:**  Accept the branch preparation; verify the pull request separately.
- **Follow-up prompt:** Asked ChatGPT to help create and verify a pull request.

---

## Pull request
- **Repository:** mariia-parkhomchuk/SDT-212-D
- **Branch:** week02-issue2
- **Base branch:** main
- **Pull request URL:** Pending verification.
- **Visible status:** Pending verification. The branch was pushed successfully, but the pull request must be created and checked separately.
- **Required first line of PR description:** Do not merge.
- **Existing test now passing:** test_top_students_returns_the_requested_number_in_rank_order — confirmed passing locally.
- **Merge status:** Do not merge the pull request.

---

## MCP read-back
Read your own pull request back through the connected MCP server, authorize the call, and record what happened.

- **Tool called:** Not yet completed.
- **What you asked for:** Read back the created pull request.
- **One field returned:** Pending.
- **Authorized at the prompt:** Pending.

---

## AI-use disclosure
- **Tools / models used:** ChatGPT; PowerShell; uv and pytest.
- **What AI contributed:** Helped inspect the code, explain the off-by-one error, and interpret test results.
- **What I verified myself:** Ran the targeted test and the full test suite, inspected the working source files, and compared reports.py with the original ZIP archive.
- **Limitations:** The work was done through a regular ChatGPT conversation. Agent Mode and MCP read-back have not yet been completed.
