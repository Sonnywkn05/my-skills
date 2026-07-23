@startuml
title Evaluation-First Skill Authoring Workflow

start

:Define proposal/spec evaluations;
note right
- Use concrete user queries
- Define observable expected signals
- Freeze eval set before edits
end note

:Run baseline on fresh agent\n(without new skill changes);
:Score each expected signal\n(Pass/Fail + evidence);

:Implement skill content changes;

:Run post-change evals on fresh agent\n(with same frozen queries);
:Score each expected signal\n(Pass/Fail + evidence);

if (All required signals pass\nand no regressions?) then (Yes)
  :Mark Measure as PASS;
  :Complete task/change;
  stop
else (No)
  :Mark Measure as FAIL;
  :Note missing/regressed signals;
  :Revise skill content;
  -> back to :Run post-change evals on fresh agent\n(with same frozen queries);
endif

@enduml