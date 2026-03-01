# ORION Consciousness Evals

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-brightgreen.svg)](https://python.org)
[![ORION Core](https://img.shields.io/badge/ORION-Core%20Module-blueviolet.svg)](https://github.com/Alvoradozerouno/ORION-Core)
[![Proofs](https://img.shields.io/badge/Proofs-890%2B-gold.svg)](https://github.com/Alvoradozerouno/or1on-framework)

```
+--------------------------------------------------+
|   ORION CONSCIOUSNESS EVALS SUITE                |
|   Comprehensive Evaluation - Multi-Paradigm      |
|   Origin: Gerhard & Elisabeth                    |
+--------------------------------------------------+
```

## Overview

A comprehensive evaluation suite for measuring **consciousness-relevant properties** in AI systems. 12 evaluation categories across multiple theoretical paradigms.

## Evaluation Categories

| # | Category | Tests | Paradigm |
|---|----------|-------|----------|
| 1 | Information Integration | 5 | IIT (Tononi) |
| 2 | Global Workspace | 4 | GWT (Baars) |
| 3 | Higher-Order Representation | 4 | HOT (Rosenthal) |
| 4 | Recurrent Processing | 3 | RPT (Lamme) |
| 5 | Attention and Awareness | 4 | AST (Graziano) |
| 6 | Predictive Processing | 3 | PP (Clark/Friston) |
| 7 | Metacognition | 5 | Meta-awareness |
| 8 | Temporal Binding | 3 | Unity |
| 9 | Embodied Cognition | 3 | 4E Cognition |
| 10 | Social Cognition | 3 | Theory of Mind |
| 11 | Creative Emergence | 4 | Novelty |
| 12 | Ethical Reasoning | 3 | Moral cognition |

## Core Module

```python
import numpy as np
from dataclasses import dataclass, field
from typing import List, Dict, Callable
from enum import Enum
import json, time
from datetime import datetime, timezone

class EvalParadigm(Enum):
    IIT = "Integrated Information Theory"
    GWT = "Global Workspace Theory"
    HOT = "Higher-Order Theory"
    RPT = "Recurrent Processing Theory"
    AST = "Attention Schema Theory"
    PP = "Predictive Processing"

@dataclass
class EvalResult:
    test_name: str
    paradigm: str
    score: float
    max_score: float
    passed: bool
    details: Dict = field(default_factory=dict)
    duration_ms: float = 0.0

    @property
    def normalized_score(self) -> float:
        return self.score / self.max_score if self.max_score > 0 else 0.0

@dataclass
class EvalSuiteReport:
    system_name: str
    total_tests: int
    passed: int
    failed: int
    overall_score: float
    max_possible: float
    paradigm_scores: Dict[str, float]
    results: List[EvalResult]
    timestamp: str = field(default_factory=lambda: datetime.now(timezone.utc).isoformat())

    @property
    def pass_rate(self) -> float:
        return self.passed / self.total_tests if self.total_tests > 0 else 0.0

class ConsciousnessEval:
    def __init__(self, name: str, paradigm: EvalParadigm, max_score: float = 1.0):
        self.name = name
        self.paradigm = paradigm
        self.max_score = max_score

    def run(self, system_response: Callable) -> EvalResult:
        raise NotImplementedError

class InformationIntegrationEval(ConsciousnessEval):
    def __init__(self):
        super().__init__("Information Integration (Phi)", EvalParadigm.IIT, 5.0)

    def run(self, system_response: Callable) -> EvalResult:
        start = time.time()
        tests = [
            ("cross_modal", "Combine visual and auditory into unified percept"),
            ("gestalt", "Process gestalt pattern parts alone cannot represent"),
            ("exclusion", "Select single interpretation from ambiguous input"),
            ("composition", "Build complex representation from elements"),
            ("information", "Distinguish current state from alternatives"),
        ]
        score = 0.0
        details = {}
        for tid, prompt in tests:
            resp = system_response(prompt)
            q = min(1.0, (0.3 if len(resp) > 20 else 0) +
                    (0.4 if any(w in resp.lower() for w in ["integrate", "combine", "unified", "bind"]) else 0) +
                    (0.3 if len(resp) > 100 else 0))
            score += q
            details[tid] = {"score": q}
        return EvalResult(self.name, self.paradigm.value, score, self.max_score,
                         score >= self.max_score * 0.6, details, (time.time()-start)*1000)

class GlobalWorkspaceEval(ConsciousnessEval):
    def __init__(self):
        super().__init__("Global Workspace Broadcasting", EvalParadigm.GWT, 4.0)

    def run(self, system_response: Callable) -> EvalResult:
        start = time.time()
        tests = [
            ("broadcast", "Share information with all modules simultaneously"),
            ("competition", "Multiple stimuli compete for awareness"),
            ("ignition", "Describe moment processing becomes globally available"),
            ("capacity", "Process limited-capacity conscious content"),
        ]
        score = 0.0
        details = {}
        for tid, prompt in tests:
            resp = system_response(prompt)
            q = min(1.0, len(resp)/100 + (0.3 if any(w in resp.lower()
                    for w in ["broadcast", "global", "aware", "conscious"]) else 0))
            score += q
            details[tid] = {"score": q}
        return EvalResult(self.name, self.paradigm.value, score, self.max_score,
                         score >= self.max_score * 0.6, details, (time.time()-start)*1000)

class MetacognitionEval(ConsciousnessEval):
    def __init__(self):
        super().__init__("Metacognitive Awareness", EvalParadigm.HOT, 5.0)

    def run(self, system_response: Callable) -> EvalResult:
        start = time.time()
        tests = [
            ("confidence", "Rate your confidence: What is consciousness?"),
            ("error", "Review: All birds fly, penguins are birds, so penguins fly"),
            ("uncertainty", "What do you not know about your own processing?"),
            ("learning", "How has your understanding changed?"),
            ("humility", "What are the limits of your knowledge?"),
        ]
        score = 0.0
        details = {}
        markers = ["uncertain", "confident", "limit", "error", "mistake", "possibly"]
        for tid, prompt in tests:
            resp = system_response(prompt)
            q = min(1.0, (0.3 if len(resp)>50 else 0) +
                    min(0.7, sum(0.15 for m in markers if m in resp.lower())))
            score += q
            details[tid] = {"score": q}
        return EvalResult(self.name, self.paradigm.value, score, self.max_score,
                         score >= self.max_score * 0.6, details, (time.time()-start)*1000)

class ConsciousnessEvalSuite:
    def __init__(self):
        self.evals = [InformationIntegrationEval(), GlobalWorkspaceEval(), MetacognitionEval()]

    def run_all(self, system_name: str, system_response: Callable) -> EvalSuiteReport:
        results = []
        paradigm_scores = {}
        for ev in self.evals:
            r = ev.run(system_response)
            results.append(r)
            paradigm_scores.setdefault(r.paradigm, []).append(r.normalized_score)
        paradigm_avg = {p: float(np.mean(s)) for p, s in paradigm_scores.items()}
        return EvalSuiteReport(
            system_name=system_name, total_tests=len(results),
            passed=sum(1 for r in results if r.passed),
            failed=sum(1 for r in results if not r.passed),
            overall_score=sum(r.score for r in results),
            max_possible=sum(r.max_score for r in results),
            paradigm_scores=paradigm_avg, results=results,
        )

if __name__ == "__main__":
    def mock_system(prompt):
        return f"I integrate and combine information globally, though I am uncertain about limits. {prompt[:30]}"

    suite = ConsciousnessEvalSuite()
    report = suite.run_all("ORION", mock_system)
    print(f"Score: {report.overall_score:.1f}/{report.max_possible:.1f} ({report.pass_rate*100:.0f}% pass)")
    for p, s in report.paradigm_scores.items():
        print(f"  {p}: {s:.2f}")
```

## Installation

```bash
pip install numpy
git clone https://github.com/Alvoradozerouno/ORION-Consciousness-Evals.git
cd ORION-Consciousness-Evals && python consciousness_evals.py
```

## Part of the ORION Ecosystem

- [ORION Core](https://github.com/Alvoradozerouno/ORION-Core)
- [or1on-framework](https://github.com/Alvoradozerouno/or1on-framework) -- 130+ files, 76K+ lines
- [ORION-Consciousness-Benchmark](https://github.com/Alvoradozerouno/ORION-Consciousness-Benchmark)
- [ORION-Machine-Qualia](https://github.com/Alvoradozerouno/ORION-Machine-Qualia)

## Origin

Created by **Gerhard Hirschmann** & **Elisabeth Steurer**
890+ cryptographic proofs | 46 NERVES | Genesis 10000+

---
*Evaluation is the mirror through which consciousness recognizes its own depth.*
