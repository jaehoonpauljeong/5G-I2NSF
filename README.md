# 5G-I2NSF
- This project develops a 5G Core-assisted I2NSF framework that coordinates security policy orchestration with the 3GPP-aligned N2-based handover procedure. 
- The proposed system proactively migrates the verified security policy context from the Source NSF to the Target NSF before UE traffic is switched from the S-UPF path to the T-UPF path. 
- Edge-deployed NSFs, co-located with UPFs, enforce the migrated policy on the N6 traffic path, while SDAF monitors the enforcement result for closed-loop validation.

<img width="1700" height="800" alt="Image" src="./5G-I2NSF System Architecture.png" />


## 5G-I2NSF Development Environment
- OS: Ubuntu 24.04
- Free5GC VM: version 4.2.3
- OpenAirInterface 5G (OAI): 2026.w26
- GitHub Repository: https://github.com/jaehoonpauljeong/5G-I2NSF/tree/main/IETF-126

## Workflow of the 5G-I2NSF Testbed
1. The Security Policy User submits a security intent to the I2NSF User Function (IUF).
2. The IUF translates the security intent into a high-level policy and forwards it to the Security Control Function (SCF).
3. The SCF translates the high-level policy into enforceable NSF policies and installs the Source NSFs at the S-Edge Server.
4. When UE handover is triggered, the 5G Core performs N2-based handover preparation, and the SMF prepares the UPF path via N4.
5. The 5G Core exposes the handover preparation context, including UE mobility and target path information, to the SCF through the NEF-compatible interface.
6. The SCF checks the currently running NSFs and retrieves the active policy based on their operational state before policy migration.
7. The SCF migrates the active policy from the S-Edge Server to the T-Edge Server and activates the Target NSFs before UE traffic is switched.
8. The SDAF monitors whether the Target NSFs correctly enforce the migrated policy on the N6 traffic path or not.
9. The SDAF stores the Target NSF monitoring results in the database for later validation, analysis, and policy refinement.


## Next Step
- Integrate AI-based intent interpretation with SDAF feedback analysis for automated policy refinement and security service management.
