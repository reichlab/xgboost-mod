# xgboost-mod
The xgboost package for gradient boosting, modified to allow inference with non-convex loss functions.

This is just a temporary storage point for this code.  Eventually, these modifications should be:
 1. merged into the latest version of xgboost
 2. added into the xgbstack package

Changes have been made to the following files:
 - src/src/tree/param.h
   - CalcGain function line 116: always calculate gain based on result of CalcWeight
   - CalcWeight function line 159: threshold hessian at 1, essentially uses linear approximation to loss if hessian is <= 1.
 - src/src/tree/updater_colmaker-inl.hpp
   - InitData function line 117: comment out things that resulted in removal of observations contributing negative values to hessian:
     - loop commented "mark delete for the deleted datas"
     - line "if (gpair[ridx].hess < 0.0f) continue;"
