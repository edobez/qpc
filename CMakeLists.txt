cmake_minimum_required(VERSION 3.0)
project(QPC)

set(QPC_COMMOM_SRCS
    src/qf/qep_hsm.c
    src/qf/qep_msm.c
    src/qf/qf_act.c 
    src/qf/qf_actq.c
    src/qf/qf_defer.c
    src/qf/qf_dyn.c
    src/qf/qf_mem.c
    src/qf/qf_ps.c
    src/qf/qf_qact.c
    src/qf/qf_qeq.c
    src/qf/qf_qmact.c
    src/qf/qf_time.c
    include/qstamp.c
)

set(QPC_COMMON_SPY_SRCS
    src/qs/qs.c
    src/qs/qs_64bit.c
    src/qs/qs_rx.c
    src/qs/qs_fp.c
)

set(POSIX_QV_PORT_SRCS
    ports/posix-qv/qf_port.c
    ports/posix-qv/qs_port.c
)

add_library(qpc STATIC
    ${QPC_COMMOM_SRCS}
    ${QPC_COMMON_SPY_SRCS}
    ${POSIX_QV_PORT_SRCS}
)

target_include_directories(qpc 
    PUBLIC
        include
    PRIVATE
        src
        ports/posix-qv
)

target_compile_definitions(qpc PRIVATE Q_SPY)

export(TARGETS qpc NAMESPACE qp:: FILE QPCTargets.cmake)
export(PACKAGE qp)