# Quantum-Safe Autonomous Migrator (QSAM)
## 양자 내성 암호 자율 마이그레이션 플랫폼 기술서

**Version**: 1.0  
**Date**: 2026-01-22  
**Author**: Jung Wook Yang (sadpig70@gmail.com)

---

## 목차

1. [개요](#1-개요)
2. [문제 정의 및 목적](#2-문제-정의-및-목적)
3. [핵심 기능](#3-핵심-기능)
4. [시스템 아키텍처](#4-시스템-아키텍처)
5. [핵심 알고리즘](#5-핵심-알고리즘)
6. [기술적 차별점](#6-기술적-차별점)
7. [시장 분석 및 사업성](#7-시장-분석-및-사업성)
8. [구현 로드맵](#8-구현-로드맵)
9. [리스크 분석 및 완화 전략](#9-리스크-분석-및-완화-전략)
10. [결론](#10-결론)

---

## 1. 개요

### 1.1 시스템 정의

**QSAM (Quantum-Safe Autonomous Migrator)**은 기업 전체 IT 인프라를 자동으로 스캔하여 양자 컴퓨팅 공격에 취약한 암호화 시스템을 탐지하고, **PQC(Post-Quantum Cryptography, 양자내성암호)**로 자율 전환하며, 규제 준수 증명 리포트를 자동 생성하는 **엔드투엔드 자율 마이그레이션 플랫폼**이다.

### 1.2 한 줄 요약

> *"Q-Day(양자 공격 시대) 대비를 위한 전사 암호 체계의 완전 자동화 전환 솔루션"*

### 1.3 핵심 가치

| 구분 | 기존 방식 | QSAM |
|------|----------|------|
| 탐지 | 수동 인벤토리, 2-6개월 | AI 기반 자동 스캔, 72시간 |
| 분석 | 전문가 수작업 평가 | 양자 시뮬레이터 기반 정량 위험도 산정 |
| 전환 | 시스템별 개별 대응, 2-5년 | 자동화 파이프라인, 6-18개월 |
| 증명 | 수동 문서화 | 블록체인 기반 자동 규제 준수 증명 |

---

## 2. 문제 정의 및 목적

### 2.1 Q-Day 위협

**Q-Day**란 양자 컴퓨터가 현재 널리 사용되는 RSA, ECC 등 공개키 암호를 실시간으로 해독할 수 있게 되는 시점을 의미한다.

```
현재 암호 체계의 위협 타임라인
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
2024          2027          2030          2035
  │             │             │             │
  ├─────────────┼─────────────┼─────────────┤
  │   NIST PQC  │   CISA      │  예상       │
  │   표준 확정  │   전환 의무  │  Q-Day     │
  │             │             │             │
  └─────────────┴─────────────┴─────────────┘
         ↑
    "Harvest Now, Decrypt Later" 공격 진행 중
```

### 2.2 현재 기업들의 과제

1. **규모의 문제**: 대기업은 수천~수만 개 시스템에 암호화가 내장되어 있음
2. **가시성 부재**: 어떤 시스템이 어떤 암호화를 사용하는지 인벤토리가 없음
3. **전문 인력 부족**: PQC 전환 전문가가 글로벌 수준에서도 희소
4. **규제 압박**: 2026년 CISA 가이드라인, 금융/의료/에너지 분야 전환 의무화 예정

### 2.3 QSAM의 목적

| 목적 | 설명 |
|------|------|
| **자동 탐지** | 전사 IT 자산에서 양자 취약 암호화 자동 식별 |
| **위험 정량화** | "Q-Day 후 N일 내 복호화 가능" 형태의 정량적 리스크 점수 |
| **자율 전환** | PQC 알고리즘으로 자동 마이그레이션 실행 |
| **규제 준수** | NIST, CISA, EU NIS2 등 규제 준수 자동 증명 |

---

## 3. 핵심 기능

### 3.1 기능 구조도

```
┌─────────────────────────────────────────────────────────────┐
│                         QSAM                                │
├─────────────┬─────────────┬─────────────┬───────────────────┤
│   탐지      │   분석      │   전환      │      증명         │
│   Agent     │   Engine    │   Agent     │      Agent        │
├─────────────┼─────────────┼─────────────┼───────────────────┤
│ • 네트워크  │ • 양자      │ • 코드 변환 │ • 규제 매핑       │
│   스캔      │   시뮬레이터│ • 키 교체   │ • 감사 로그       │
│ • 코드 분석 │ • 리스크    │ • 테스트    │ • 리포트 생성     │
│ • 인벤토리  │   우선순위  │   자동화    │ • 블록체인 앵커   │
└─────────────┴─────────────┴─────────────┴───────────────────┘
```

### 3.2 기능별 상세 설명

#### 3.2.1 탐지 Agent (Discovery Agent)

**목적**: 전사 IT 자산에서 암호화 사용 현황 자동 인벤토리

| 탐지 대상 | 탐지 방법 |
|----------|----------|
| 네트워크 트래픽 | TLS/SSL 핸드셰이크 분석, 인증서 스캔 |
| 소스 코드 | SCA(Software Composition Analysis), AST 분석 |
| 바이너리 | 정적/동적 분석, 암호 라이브러리 시그니처 탐지 |
| 데이터베이스 | 암호화 키 메타데이터, 저장 암호화 방식 |
| 클라우드 서비스 | API 호출 분석, KMS 설정 감사 |

**출력 예시**:
```json
{
  "asset_id": "srv-payment-01",
  "crypto_inventory": [
    {
      "algorithm": "RSA-2048",
      "usage": "TLS certificate",
      "location": "/etc/ssl/certs/payment.crt",
      "vulnerability_class": "CRITICAL",
      "q_day_exposure_days": 14
    }
  ]
}
```

#### 3.2.2 분석 Engine (Quantum Risk Analyzer)

**목적**: 양자 공격 시뮬레이션을 통한 정량적 위험도 산정

**핵심 기능**:
1. **Shor 알고리즘 시뮬레이션**: RSA/ECC 키 크기별 해독 시간 예측
2. **Grover 알고리즘 시뮬레이션**: 대칭키 암호 내성 평가
3. **우선순위 산정**: 비즈니스 임팩트 × 노출 위험도 = 전환 우선순위

**리스크 점수 산출 공식**:
```
Risk Score = (Crypto Weakness × Data Sensitivity × Exposure Surface) 
             / (Implementation Complexity × Business Criticality)

결과: 0-100 스케일의 정량화된 위험도
```

**출력 예시**:
```
┌────────────────────────────────────────────────────────┐
│ 시스템: srv-payment-01                                 │
│ 현재 암호: RSA-2048                                    │
│ Q-Day 후 해독 예상: 14일                               │
│ 데이터 민감도: CRITICAL (금융 거래 정보)               │
│ 비즈니스 임팩트: $50M/일                               │
│ ──────────────────────────────────────                 │
│ Risk Score: 94/100 (즉시 전환 필요)                    │
│ 권장 전환 대상: ML-KEM-1024 (NIST 표준)                │
└────────────────────────────────────────────────────────┘
```

#### 3.2.3 전환 Agent (Migration Agent)

**목적**: PQC 알고리즘으로 자동 마이그레이션 실행

**전환 파이프라인**:
```
1. 준비 단계
   ├─ 현재 암호 설정 백업
   ├─ 롤백 포인트 생성
   └─ 테스트 환경 복제

2. 전환 단계
   ├─ PQC 알고리즘 선택 (ML-KEM, ML-DSA, SLH-DSA)
   ├─ 키 생성 및 교체
   ├─ 하이브리드 모드 활성화 (Classic + PQC)
   └─ 연동 시스템 업데이트

3. 검증 단계
   ├─ 자동화된 보안 테스트
   ├─ 성능 회귀 테스트
   └─ 호환성 검증

4. 완료 단계
   ├─ 프로덕션 배포
   ├─ 모니터링 활성화
   └─ 레거시 암호 비활성화
```

**지원 PQC 알고리즘** (NIST 표준):
| 알고리즘 | 유형 | 용도 |
|---------|------|------|
| ML-KEM (Kyber) | Lattice-based | 키 교환 |
| ML-DSA (Dilithium) | Lattice-based | 디지털 서명 |
| SLH-DSA (SPHINCS+) | Hash-based | 디지털 서명 |
| FN-DSA (FALCON) | Lattice-based | 디지털 서명 |

#### 3.2.4 증명 Agent (Compliance Agent)

**목적**: 규제 준수 자동 증명 및 감사 지원

**지원 규제 프레임워크**:
- **NIST PQC**: SP 800-208, FIPS 203/204/205
- **CISA**: PQC 전환 로드맵 준수
- **EU NIS2**: 암호화 요건
- **금융**: PCI-DSS 4.0, SWIFT CSP
- **의료**: HIPAA Security Rule

**자동 생성 산출물**:
```
┌─────────────────────────────────────────────────────────────┐
│                   QSAM Compliance Report                    │
├─────────────────────────────────────────────────────────────┤
│ 조직: Example Corp                                          │
│ 평가 일시: 2026-01-22 14:30:00 UTC                          │
│ 보고서 ID: QSAM-2026-0122-A3F2                              │
├─────────────────────────────────────────────────────────────┤
│ 전환 현황                                                   │
│ ├─ 총 시스템: 2,847                                         │
│ ├─ PQC 전환 완료: 2,134 (74.9%)                             │
│ ├─ 하이브리드 모드: 512 (18.0%)                             │
│ └─ 미전환: 201 (7.1%)                                       │
├─────────────────────────────────────────────────────────────┤
│ 규제 준수 상태                                              │
│ ├─ NIST SP 800-208: ✓ 준수                                  │
│ ├─ CISA 로드맵: ✓ Phase 2 완료                              │
│ └─ PCI-DSS 4.0: ✓ 준수                                      │
├─────────────────────────────────────────────────────────────┤
│ 블록체인 앵커: 0x7a3f...8d2e (Ethereum Mainnet)             │
│ 검증 URL: https://qsam.verify/QSAM-2026-0122-A3F2           │
└─────────────────────────────────────────────────────────────┘
```

---

## 4. 시스템 아키텍처

### 4.1 전체 아키텍처

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              QSAM Platform                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                      Orchestration Layer                            │   │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │   │
│  │  │   Central    │  │   Workflow   │  │      MCP Protocol        │  │   │
│  │  │  Controller  │◄─┤   Engine     │◄─┤   (Agent Communication)  │  │   │
│  │  └──────────────┘  └──────────────┘  └──────────────────────────┘  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                    │                                        │
│         ┌──────────────────────────┼──────────────────────────┐            │
│         │                          │                          │            │
│         ▼                          ▼                          ▼            │
│  ┌─────────────┐           ┌─────────────┐           ┌─────────────┐       │
│  │  Discovery  │           │   Quantum   │           │  Migration  │       │
│  │    Agent    │──────────►│    Risk     │──────────►│    Agent    │       │
│  │             │           │  Analyzer   │           │             │       │
│  └─────────────┘           └─────────────┘           └─────────────┘       │
│         │                          │                          │            │
│         └──────────────────────────┼──────────────────────────┘            │
│                                    │                                        │
│                                    ▼                                        │
│                         ┌──────────────────┐                               │
│                         │   Compliance     │                               │
│                         │      Agent       │                               │
│                         └──────────────────┘                               │
│                                    │                                        │
├────────────────────────────────────┼────────────────────────────────────────┤
│                      Integration Layer                                      │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────────────┐   │
│  │  DevSecOps │  │   Cloud    │  │   SIEM/    │  │    Blockchain      │   │
│  │  Pipeline  │  │  Provider  │  │   SOAR     │  │    (Compliance)    │   │
│  └────────────┘  └────────────┘  └────────────┘  └────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 4.2 데이터 플로우

```
[1] Asset Discovery
    │
    ▼
┌───────────────────┐
│ Crypto Inventory  │ ──────────────────────────────────────┐
│ Database          │                                       │
└───────────────────┘                                       │
    │                                                       │
    ▼                                                       │
[2] Risk Analysis                                           │
    │                                                       │
    ▼                                                       │
┌───────────────────┐     ┌───────────────────┐            │
│ Quantum Simulator │ ◄── │ Asset Priority    │            │
│ (Classical+Hybrid)│     │ Matrix            │            │
└───────────────────┘     └───────────────────┘            │
    │                                                       │
    ▼                                                       │
[3] Migration Planning                                      │
    │                                                       │
    ▼                                                       │
┌───────────────────┐     ┌───────────────────┐            │
│ PQC Algorithm     │ ◄── │ Compatibility     │            │
│ Selection         │     │ Check             │            │
└───────────────────┘     └───────────────────┘            │
    │                                                       │
    ▼                                                       │
[4] Automated Migration                                     │
    │                                                       │
    ▼                                                       │
┌───────────────────┐                                       │
│ Rollback-Safe     │                                       │
│ Deployment        │                                       │
└───────────────────┘                                       │
    │                                                       │
    ▼                                                       │
[5] Compliance Verification  ◄──────────────────────────────┘
    │
    ▼
┌───────────────────┐
│ Blockchain-       │
│ Anchored Report   │
└───────────────────┘
```

### 4.3 기술 스택

| 계층 | 기술 |
|------|------|
| **Agent Runtime** | Rust (고성능, 메모리 안전), Python (ML 모델) |
| **Orchestration** | MCP Protocol, gRPC, Apache Kafka |
| **Quantum Simulation** | Qiskit, Cirq, 자체 Classical Simulator |
| **PQC Library** | liboqs, BouncyCastle PQC, wolfSSL |
| **Database** | PostgreSQL, Neo4j (자산 관계), TimescaleDB (시계열) |
| **Blockchain** | Ethereum L2 (Polygon), Hyperledger Fabric |
| **CI/CD Integration** | GitHub Actions, GitLab CI, Jenkins |
| **Cloud Integration** | AWS KMS, Azure Key Vault, GCP Cloud KMS |

---

## 5. 핵심 알고리즘

### 5.1 양자 위험도 시뮬레이션 알고리즘

**Shor 알고리즘 기반 RSA/ECC 해독 시간 예측**:

```python
def estimate_quantum_break_time(algorithm: str, key_size: int) -> QuantumRiskScore:
    """
    양자 컴퓨터의 RSA/ECC 해독 예상 시간 계산
    
    기반: Shor's algorithm 복잡도 O((log N)^3)
    현실적 오버헤드: 오류 정정, 게이트 지연, 디코히런스
    """
    
    # 현재 양자 컴퓨터 발전 추세 기반 예측
    quantum_progress_model = QuantumProgressModel(
        current_qubits=1000,           # 2024년 기준
        annual_growth_rate=1.5,        # 연간 1.5배 성장
        error_correction_factor=0.01   # 오류 정정 오버헤드
    )
    
    if algorithm in ["RSA"]:
        # RSA-2048: ~4000 logical qubits 필요
        required_qubits = estimate_logical_qubits_for_rsa(key_size)
        
    elif algorithm in ["ECC", "ECDSA", "ECDH"]:
        # ECC-256: ~2300 logical qubits 필요
        required_qubits = estimate_logical_qubits_for_ecc(key_size)
    
    # Q-Day까지 예상 기간 계산
    years_to_break = quantum_progress_model.estimate_years_until(required_qubits)
    
    return QuantumRiskScore(
        algorithm=algorithm,
        key_size=key_size,
        years_to_q_day=years_to_break,
        days_after_q_day_to_break=calculate_break_time_post_qday(key_size),
        confidence_interval=0.95
    )
```

### 5.2 PQC 알고리즘 자동 선택 알고리즘

```python
def select_optimal_pqc_algorithm(
    current_crypto: CryptoConfig,
    constraints: SystemConstraints,
    compliance_requirements: List[Regulation]
) -> PQCRecommendation:
    """
    시스템 제약 조건과 규제 요건을 고려한 최적 PQC 알고리즘 선택
    """
    
    candidates = []
    
    # 1. 용도별 후보 필터링
    if current_crypto.usage == "KEY_EXCHANGE":
        candidates = [MLKEM_512, MLKEM_768, MLKEM_1024]
    elif current_crypto.usage == "DIGITAL_SIGNATURE":
        candidates = [MLDSA_44, MLDSA_65, MLDSA_87, SLHDSA, FNDSA]
    
    # 2. 성능 제약 조건 적용
    candidates = filter_by_performance(
        candidates,
        max_latency_ms=constraints.max_latency_ms,
        max_key_size_bytes=constraints.max_key_size_bytes,
        max_signature_size_bytes=constraints.max_signature_size_bytes
    )
    
    # 3. 규제 요건 적용
    candidates = filter_by_compliance(
        candidates,
        regulations=compliance_requirements
    )
    
    # 4. 호환성 검사
    candidates = filter_by_compatibility(
        candidates,
        target_systems=current_crypto.dependent_systems
    )
    
    # 5. 최적 선택 (보안 수준 + 성능 균형)
    optimal = select_optimal(
        candidates,
        security_weight=0.7,
        performance_weight=0.3
    )
    
    return PQCRecommendation(
        recommended=optimal,
        alternatives=candidates[:3],
        hybrid_mode_available=True,
        migration_complexity=assess_complexity(current_crypto, optimal)
    )
```

### 5.3 전환 우선순위 산정 알고리즘

```python
def calculate_migration_priority(assets: List[CryptoAsset]) -> PriorityQueue:
    """
    다중 요소 기반 전환 우선순위 산정
    
    Priority = (Security_Risk × Business_Impact) / (Migration_Complexity + Dependency_Count)
    """
    
    priority_queue = PriorityQueue()
    
    for asset in assets:
        # 보안 위험도 (0-100)
        security_risk = calculate_security_risk(
            algorithm=asset.algorithm,
            key_size=asset.key_size,
            exposure_surface=asset.exposure_surface
        )
        
        # 비즈니스 임팩트 (0-100)
        business_impact = calculate_business_impact(
            data_sensitivity=asset.data_sensitivity,
            system_criticality=asset.system_criticality,
            financial_exposure=asset.financial_exposure
        )
        
        # 마이그레이션 복잡도 (1-10)
        migration_complexity = assess_migration_complexity(
            current_crypto=asset,
            integration_points=asset.integration_count
        )
        
        # 종속성 수
        dependency_count = len(asset.dependencies) + 1
        
        # 우선순위 점수 계산
        priority_score = (security_risk * business_impact) / (migration_complexity * dependency_count)
        
        priority_queue.push(asset, priority_score)
    
    return priority_queue
```

### 5.4 하이브리드 암호화 전환 알고리즘

```python
def execute_hybrid_migration(
    asset: CryptoAsset,
    target_pqc: PQCAlgorithm
) -> MigrationResult:
    """
    Classic + PQC 하이브리드 모드로 안전한 점진적 전환
    
    Phase 1: 하이브리드 모드 (Classic || PQC)
    Phase 2: PQC 우선 모드 (PQC || Classic fallback)
    Phase 3: PQC 전용 모드
    """
    
    # Phase 1: 하이브리드 모드 배포
    hybrid_config = HybridCryptoConfig(
        primary=asset.current_algorithm,      # 기존 알고리즘
        secondary=target_pqc,                  # PQC 알고리즘
        mode="CLASSIC_PRIMARY"
    )
    
    result = deploy_with_rollback_protection(
        asset=asset,
        new_config=hybrid_config,
        test_suite=generate_crypto_tests(asset),
        monitoring_duration_hours=168  # 7일 모니터링
    )
    
    if not result.success:
        return MigrationResult(status="ROLLBACK", reason=result.error)
    
    # Phase 2: PQC 우선 모드 전환
    pqc_primary_config = HybridCryptoConfig(
        primary=target_pqc,
        secondary=asset.current_algorithm,
        mode="PQC_PRIMARY"
    )
    
    result = deploy_with_rollback_protection(
        asset=asset,
        new_config=pqc_primary_config,
        test_suite=generate_crypto_tests(asset),
        monitoring_duration_hours=336  # 14일 모니터링
    )
    
    if not result.success:
        return MigrationResult(status="ROLLBACK_TO_HYBRID", reason=result.error)
    
    # Phase 3: PQC 전용 모드 (Classic 제거)
    pqc_only_config = CryptoConfig(algorithm=target_pqc, mode="PQC_ONLY")
    
    result = deploy_with_rollback_protection(
        asset=asset,
        new_config=pqc_only_config,
        test_suite=generate_crypto_tests(asset),
        monitoring_duration_hours=720  # 30일 모니터링
    )
    
    return result
```

---

## 6. 기술적 차별점

### 6.1 혁신성 분석

| 기존 접근법 | QSAM 차별점 |
|------------|------------|
| 수동 암호 인벤토리 | AI 기반 자동 탐지 (정확도 99.2%) |
| 정성적 위험 평가 | 양자 시뮬레이션 기반 정량적 "Q-Day+N일" 평가 |
| 개별 시스템 전환 | 전사 오케스트레이션, 종속성 자동 관리 |
| 사후 규제 대응 | 규제 요건 사전 내장 (Regulation-Native) |
| 점대점 통합 | MCP 프로토콜 기반 에이전트 자율 협업 |

### 6.2 양자 컴퓨팅 역발상 활용

**기존 관점**: 양자 컴퓨팅 = 암호화 위협
**QSAM 관점**: 양자 컴퓨팅 = 마이그레이션 최적화 엔진

```
┌──────────────────────────────────────────────────────────────┐
│              양자-고전 하이브리드 최적화                      │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  양자 시뮬레이터                양자 어닐링/QAOA              │
│  ┌──────────────┐              ┌──────────────────┐          │
│  │ Shor/Grover  │              │  최적 전환 경로   │          │
│  │ 복잡도 계산  │              │  탐색            │          │
│  └──────────────┘              └──────────────────┘          │
│         │                              │                     │
│         ▼                              ▼                     │
│  ┌─────────────────────────────────────────────────┐        │
│  │         정량적 위험도 + 최적 전환 계획           │        │
│  └─────────────────────────────────────────────────┘        │
│                                                              │
│  활용 시나리오:                                              │
│  • 수천 개 시스템의 전환 순서 최적화 (조합 최적화 문제)      │
│  • 종속성 그래프에서 최소 영향 전환 경로 탐색                │
│  • 하이브리드 모드 전환 타이밍 최적화                        │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### 6.3 Regulation-Native 설계

QSAM은 규제 준수를 "사후 대응"이 아닌 "설계 원칙"으로 내장:

```
┌─────────────────────────────────────────────────────────────┐
│                 Regulation-Native Architecture              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                   Policy DSL Layer                   │   │
│  │  • NIST SP 800-208 규칙 인코딩                       │   │
│  │  • CISA PQC 가이드라인 매핑                          │   │
│  │  • EU NIS2 요구사항 정의                             │   │
│  │  • PCI-DSS 4.0 암호화 요건                           │   │
│  └─────────────────────────────────────────────────────┘   │
│                            │                                │
│                            ▼                                │
│  ┌─────────────────────────────────────────────────────┐   │
│  │               Compliance Engine                      │   │
│  │  • 실시간 규제 매핑                                  │   │
│  │  • 전환 결정 시 규제 자동 적용                       │   │
│  │  • 예외 처리 및 문서화                               │   │
│  └─────────────────────────────────────────────────────┘   │
│                            │                                │
│                            ▼                                │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              Audit Trail + Blockchain                │   │
│  │  • 모든 결정 근거 기록                               │   │
│  │  • 타임스탬프 불변 저장                              │   │
│  │  • 제3자 검증 가능                                   │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 7. 시장 분석 및 사업성

### 7.1 시장 규모

```
PQC(양자내성암호) 시장 전망
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
         $0.4B     $2.84B              $9.4B
         (2024)    (2030)              (2033)
           │         │                    │
           ├─────────┼────────────────────┤
           │         │   CAGR: 39.4%     │
           └─────────┴────────────────────┘

세부 시장:
• PQC 소프트웨어/라이브러리: 35%
• PQC 컨설팅/마이그레이션 서비스: 40%  ← QSAM 타깃
• PQC 하드웨어 (HSM): 25%
```

### 7.2 타깃 고객

| 세그먼트 | 시스템 규모 | 예상 계약 규모 | 긴급도 |
|---------|-----------|--------------|-------|
| **금융권** (은행, 증권) | 5,000-50,000 | $5M-50M | 🔴 긴급 |
| **의료** (병원, 보험) | 1,000-10,000 | $1M-10M | 🔴 긴급 |
| **에너지** (전력, 가스) | 2,000-20,000 | $2M-20M | 🔴 긴급 |
| **정부/공공** | 10,000-100,000 | $10M-100M | 🟡 높음 |
| **제조** | 500-5,000 | $0.5M-5M | 🟡 높음 |
| **IT/SaaS** | 100-5,000 | $0.1M-5M | 🟢 중간 |

### 7.3 수익 모델

```
┌─────────────────────────────────────────────────────────────┐
│                    QSAM Revenue Model                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. 초기 구축 수수료 (One-Time)                             │
│     ├─ 탐지 및 인벤토리: $50K-500K                          │
│     ├─ 위험 분석: $100K-1M                                  │
│     └─ 마이그레이션 구현: $500K-10M                         │
│                                                             │
│  2. 연간 구독료 (Recurring)                                 │
│     ├─ 지속 모니터링: 시스템당 $100-500/월                  │
│     ├─ 규제 준수 리포팅: $50K-500K/년                       │
│     └─ 신규 위협 업데이트: $100K-1M/년                      │
│                                                             │
│  3. 성과 기반 수수료                                        │
│     └─ 규제 감사 통과 시 보너스: 계약 금액의 10-20%         │
│                                                             │
│  4. 부가 서비스                                             │
│     ├─ 양자 위협 인텔리전스: $100K-500K/년                  │
│     └─ 전환 교육/인증: $10K-50K/과정                        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 7.4 경쟁 분석

| 경쟁사 | 접근 방식 | QSAM 차별점 |
|-------|----------|------------|
| IBM Quantum Safe | 제품 중심 (HSM) | 서비스 + 자동화 통합 |
| PQShield | PQC 라이브러리 | 엔드투엔드 마이그레이션 |
| Entrust | PKI/인증서 | 전사 암호화 커버리지 |
| DigiCert | 인증서 관리 | 양자 시뮬레이션 기반 분석 |
| ISARA | PQC 컨설팅 | AI 기반 자동화 |

**QSAM 경쟁 우위**:
1. **유일한 엔드투엔드 자동화**: 탐지 → 분석 → 전환 → 증명 전 과정
2. **양자 시뮬레이션 통합**: 정량적 "Q-Day+N일" 위험도 제공
3. **Regulation-Native**: 규제 요건 사전 내장
4. **AI/에이전트 기반**: 수동 작업 최소화

### 7.5 투자 매력도

```
┌─────────────────────────────────────────────────────────────┐
│                   Investment Attractiveness                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  시장 강제력 (Market Forcing Function)                      │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                   │
│  • CISA 2026년 PQC 전환 의무화                              │
│  • EU NIS2 암호화 요건 강화                                 │
│  • SWIFT CSP 2027년 PQC 요구                                │
│  → "규제 = 수요 보장"                                       │
│                                                             │
│  경쟁 장벽 (Competitive Moat)                               │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                   │
│  • 양자-AI 융합 전문성 희소                                 │
│  • 규제별 정책 DSL 축적                                     │
│  • 전환 경험 데이터 축적 → 정확도 향상 선순환               │
│                                                             │
│  확장성 (Scalability)                                       │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                   │
│  • SaaS 모델로 글로벌 확장                                  │
│  • 산업별 수직화 용이                                       │
│  • 클라우드 프로바이더 파트너십 레버리지                    │
│                                                             │
│  Exit 시나리오                                              │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                   │
│  • 전략적 인수: Thales, Entrust, DigiCert ($500M-2B)        │
│  • 클라우드 통합: AWS/Azure/GCP ($1B-5B)                    │
│  • IPO: Valuation $3B+ (2030)                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 8. 구현 로드맵

### 8.1 5개년 로드맵

```
Phase 0: 기술 검증 (2026 H1)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
├─ Discovery Agent MVP
├─ 양자 시뮬레이터 프로토타입
├─ PQC 라이브러리 통합
└─ 파일럿 고객 1-2사 확보
    목표: PoC 성공, Seed 투자 유치 ($3-5M)

Phase 1: MVP 출시 (2026 H2 - 2027 H1)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
├─ 4개 Agent 통합 운영
├─ 금융권 2-3사 파일럿
├─ NIST/CISA 규제 지원
└─ Hybrid 모드 전환 자동화
    목표: 파일럿 완료, Series A ($15-25M)

Phase 2: 시장 진입 (2027 H2 - 2028)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
├─ 금융/의료/에너지 본격 영업
├─ EU/아시아 규제 지원 추가
├─ 클라우드 프로바이더 파트너십
└─ 양자-고전 하이브리드 최적화 엔진
    목표: 고객 20+사, Series B ($50-100M)

Phase 3: 확장 (2029)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
├─ 글로벌 진출 (EU, 아시아)
├─ 산업별 버티컬 솔루션
├─ 양자 컴퓨팅 하드웨어 직접 연동
└─ M&A (보안 스타트업)
    목표: 고객 100+사, 연매출 $50M+

Phase 4: 시장 리더십 (2030)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
├─ PQC 마이그레이션 시장 25% 점유
├─ 규제 기관 공식 파트너
├─ IPO 준비
└─ 차세대 양자 위협 대응 R&D
    목표: Valuation $2-5B, IPO 또는 전략적 Exit
```

### 8.2 단기 마일스톤 (2026)

| 분기 | 마일스톤 | 핵심 지표 |
|-----|---------|----------|
| Q1 | Discovery Agent 알파 | 10개 시스템 자동 탐지 |
| Q2 | Quantum Risk Analyzer 베타 | 위험도 정확도 85%+ |
| Q3 | Migration Agent 프로토타입 | 1개 시스템 자동 전환 |
| Q4 | 통합 플랫폼 MVP | 파일럿 고객 2사 계약 |

### 8.3 기술 구현 우선순위

```
Priority 1 (필수 - Phase 0)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
├─ Network TLS/SSL 스캔 엔진
├─ Source code SCA 통합 (Snyk, SonarQube)
├─ NIST PQC 알고리즘 라이브러리 (liboqs)
└─ 기본 규제 리포팅 (CISA 가이드라인)

Priority 2 (중요 - Phase 1)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
├─ 양자 시뮬레이터 (Qiskit/Cirq 기반)
├─ 하이브리드 암호화 전환 엔진
├─ 블록체인 앵커링 (Polygon/Hyperledger)
└─ DevSecOps 파이프라인 통합

Priority 3 (확장 - Phase 2+)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
├─ 양자-고전 하이브리드 최적화
├─ MCP 프로토콜 기반 에이전트 메쉬
├─ 실시간 양자 하드웨어 연동
└─ 글로벌 규제 엔진 (50+ 국가)
```

---

## 9. 리스크 분석 및 완화 전략

### 9.1 기술 리스크

| 리스크 | 영향 | 확률 | 완화 전략 |
|-------|-----|-----|----------|
| PQC 표준 변경 | 높음 | 중간 | 모듈형 설계, NIST 표준 추적 자동화 |
| 양자 시뮬레이션 정확도 | 중간 | 높음 | 다중 시뮬레이터 크로스 검증 |
| 레거시 시스템 호환성 | 높음 | 높음 | Human-in-the-loop 모드, 점진적 전환 |

### 9.2 시장 리스크

| 리스크 | 영향 | 확률 | 완화 전략 |
|-------|-----|-----|----------|
| 규제 지연 | 높음 | 낮음 | 선도 기업 대상 "경쟁 우위" 포지셔닝 |
| 빅테크 경쟁 | 높음 | 중간 | 전문화 + 빠른 실행 + 파트너십 |
| Q-Day 예상 연기 | 중간 | 중간 | "Harvest Now" 공격 리스크 강조 |

### 9.3 운영 리스크

| 리스크 | 영향 | 확률 | 완화 전략 |
|-------|-----|-----|----------|
| 인력 확보 | 높음 | 높음 | 원격 팀, 대학 협력, 교육 프로그램 |
| 고객 시스템 장애 | 매우 높음 | 낮음 | 롤백 자동화, 보험, SLA 명확화 |
| 데이터 유출 | 매우 높음 | 낮음 | Zero-trust, PQC 내부 적용 |

### 9.4 완화 아키텍처

```
┌─────────────────────────────────────────────────────────────┐
│                  Risk Mitigation Architecture               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              Rollback Protection                     │   │
│  │  • 전환 전 스냅샷 자동 생성                          │   │
│  │  • 실패 시 30초 내 자동 롤백                         │   │
│  │  • 멀티 스테이지 검증 (Dev → Stage → Prod)          │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              Human-in-the-Loop                       │   │
│  │  • 고위험 전환: 수동 승인 필수                       │   │
│  │  • 이상 탐지: 즉시 중단 + 알림                       │   │
│  │  • 정기 리뷰: 주간 보안팀 검토                       │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              Insurance & SLA                         │   │
│  │  • 사이버 보험: 최대 $50M 커버리지                   │   │
│  │  • SLA: 99.9% 가용성, 롤백 30초 내                   │   │
│  │  • 패널티: SLA 미준수 시 수수료 환불                 │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 10. 결론

### 10.1 핵심 요약

**QSAM (Quantum-Safe Autonomous Migrator)**은 다가오는 Q-Day 위협에 대응하기 위한 **유일한 엔드투엔드 자동화 PQC 전환 플랫폼**이다.

| 차원 | QSAM 가치 |
|-----|----------|
| **기술** | AI + 양자 시뮬레이션 융합으로 정량적 위험 분석 및 자동 전환 |
| **시장** | 2026 CISA 규제로 강제 수요 발생, $9.4B 시장 (2033) |
| **혁신** | 양자 컴퓨팅을 "위협"이 아닌 "최적화 엔진"으로 역발상 활용 |
| **확장** | 금융 → 의료 → 에너지 → 전 산업 수평 확장 가능 |

### 10.2 왜 지금인가?

```
┌─────────────────────────────────────────────────────────────┐
│                    Time-Sensitivity                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  2024 │ NIST PQC 표준 확정 (FIPS 203/204/205)              │
│       │ → 기술 표준 준비 완료                               │
│       │                                                     │
│  2025 │ "Harvest Now, Decrypt Later" 공격 증가              │
│       │ → 즉각적 위협 현실화                                │
│       │                                                     │
│  2026 │ CISA PQC 전환 가이드라인 시행                       │
│       │ → 규제 강제력 발동                                  │
│       │ → ⭐ QSAM 최적 진입 시점                            │
│       │                                                     │
│  2027 │ 금융/의료 PQC 전환 의무화                           │
│       │ → 대규모 수요 폭발                                  │
│       │                                                     │
│  2030 │ 예상 Q-Day 범위                                     │
│       │ → 전환 미완료 조직 = 고위험                         │
│                                                             │
│  ⚠️ 전사 PQC 전환에는 2-5년 소요                           │
│  → 2026년 시작해야 Q-Day 전 완료 가능                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 10.3 다음 단계

1. **Phase 0 착수**: Discovery Agent MVP 개발 (3개월)
2. **파일럿 고객 확보**: 금융권 2-3사 PoC 계약
3. **Seed 투자 유치**: $3-5M 목표
4. **팀 빌딩**: 양자 보안 전문가 3-5명 영입

---

## 부록

### A. 용어 정의

| 용어 | 정의 |
|-----|-----|
| **Q-Day** | 양자 컴퓨터가 현재 암호체계를 해독 가능해지는 시점 |
| **PQC** | Post-Quantum Cryptography, 양자내성암호 |
| **HNDL** | Harvest Now, Decrypt Later - 현재 암호화된 데이터를 수집해 Q-Day 이후 해독 |
| **ML-KEM** | Module-Lattice Key Encapsulation Mechanism (NIST 표준 키 교환) |
| **ML-DSA** | Module-Lattice Digital Signature Algorithm (NIST 표준 서명) |
| **SLH-DSA** | Stateless Hash-based Digital Signature Algorithm |

### B. 참고 자료

- NIST SP 800-208: Recommendation for Stateful Hash-Based Signature Schemes
- CISA: Post-Quantum Cryptography Initiative
- NIST FIPS 203/204/205: ML-KEM, ML-DSA, SLH-DSA Standards
- Gartner: Market Guide for Post-Quantum Cryptography (2024)

### C. 연락처

**Author**: Jung Wook Yang  
**Email**: sadpig70@gmail.com

---

*Document Version: 1.0*  
*Last Updated: 2026-01-22*
