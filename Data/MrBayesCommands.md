#**Substitution Models**

##GTR

    lset applyto=() nst=6                           # GTR
    
    lset applyto=() nst=6 rates=propinv             # GTR + I
    
    lset applyto=() nst=6 rates=gamma               # GTR + gamma
    
    lset applyto=() nst=6 rates=invgamma            # GTR + I + gamma

##SYM

    lset applyto=() nst=6                           # SYM
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=6 rates=propinv             # SYM + I
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=6 rates=gamma               # SYM + gamma
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=6 rates=invgamma            # SYM + I + gamma
    prset applyto=() statefreqpr=fixed(equal)


##HKY

    lset applyto=() nst=2                           # HKY
    lset applyto=() nst=2 rates=propinv             # HKY + I
    lset applyto=() nst=2 rates=gamma               # HKY + gamma
    lset applyto=() nst=2 rates=invgamma            # HKY + I + gamma

##K2P

    lset applyto=() nst=2                           # K2P
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=2 rates=propinv             # K2P + I
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=2 rates=gamma               # K2P + gamma
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=2 rates=invgamma            # K2P + I + gamma
    prset applyto=() statefreqpr=fixed(equal)


##F81

    lset applyto=() nst=1                           # F81
    lset applyto=() nst=1 rates=propinv             # F81 + I
    lset applyto=() nst=1 rates=gamma               # F81 + gamma
    lset applyto=() nst=1 rates=invgamma            # F81 + I + gamma

## Jukes Cantor  

    lset applyto=() nst=1                           # JC
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=1 rates=propinv             # JC + I
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=1 rates=gamma               # JC + gamma
    prset applyto=() statefreqpr=fixed(equal)

    lset applyto=() nst=1 rates=incgamma            # JC + I + gamma
    prset applyto=() statefreqpr=fixed(equal)
