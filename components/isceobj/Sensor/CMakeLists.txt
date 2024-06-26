add_subdirectory(db)
add_subdirectory(TOPS)
add_subdirectory(MultiMode)
add_subdirectory(GRD)
isce2_add_cdll(envisat src/asa_im_decode/asa_im_decode.c)

set(installfiles
    alos
    cosar
    envisat
    __init__.py
    ALOS.py
    ALOS2.py
    ALOS_SLC.py
    CEOS.py
    COSMO_SkyMed.py
    COSMO_SkyMed_SLC.py
    ERS.py
    ERS_EnviSAT.py
    ERS_EnviSAT_SLC.py
    ERS_SLC.py
    EnviSAT.py
    EnviSAT_SLC.py
    Generic.py
    ICEYE_SLC.py
    JERS.py
    KOMPSAT5.py
    Polarimetry.py
    ROI_PAC.py
    Radarsat1.py
    Radarsat2.py
    Risat1.py
    Risat1_SLC.py
    SICD_RGZERO.py
    Sensor.py
    Sentinel1.py
    TanDEMX.py
    TerraSARX.py
    UAVSAR_HDF5_SLC.py
    UAVSAR_Polsar.py
    UAVSAR_RPI.py
    UAVSAR_Stack.py
    SAOCOM_SLC.py
    Lutan1.py
    )

if(HDF5_FOUND)
    Python_add_library(csk MODULE
        src/extract_csk/extract_csk.c
        src/extract_csk/extract_csk_slc.c
        )
    target_include_directories(csk PUBLIC include)
    target_link_libraries(csk PUBLIC HDF5::HDF5)
    list(APPEND installfiles csk)
endif()

Python_add_library(alos MODULE
    bindings/alosmodule.cpp
    src/ALOS_pre_process/lib_functions.h
    src/ALOS_pre_process/read_ALOSE_data.c
    src/ALOS_pre_process/siocomplex.h
    src/ALOS_pre_process/utils.c
    src/ALOS_pre_process/ALOSE_orbits_utils.c
    src/ALOS_pre_process/ALOS_ldr_orbit.c
    src/ALOS_pre_process/ALOS_pre_process.c
    src/ALOS_pre_process/calc_dop.c
    src/ALOS_pre_process/data_ALOS.h
    src/ALOS_pre_process/data_ALOSE.h
    src/ALOS_pre_process/hermite_c.c
    src/ALOS_pre_process/image_sio.c
    src/ALOS_pre_process/init_from_PRM.c
    src/ALOS_pre_process/interpolate_ALOS_orbit.c
    src/ALOS_pre_process/null_sio_struct.c
    src/ALOS_pre_process/orbit_ALOS.h
    src/ALOS_pre_process/parse_ALOS_commands.c
    src/ALOS_pre_process/polyfit.c
    src/ALOS_pre_process/readOrbitPulseSetState.f
    src/ALOS_pre_process/readOrbitPulseState.f
    src/ALOS_pre_process/read_ALOS_data.c
    src/ALOS_pre_process/read_ALOS_sarleader.c
    src/ALOS_pre_process/roi_utils.c
    src/ALOS_pre_process/sarleader_ALOS.h
    src/ALOS_pre_process/sarleader_fdr.h
    src/ALOS_pre_process/set_ALOS_defaults.c
    src/ALOS_pre_process/siocomplex.c
    src/ALOS_pre_process/swap_ALOS_data_info.c
    src/ALOS_pre_process/write_ALOS_prm.c
    src/ALOS_pre_process/readOrbitPulse.f
    src/ALOS_pre_process/get_sio_struct.c
    src/ALOS_pre_process/lib_array.c
    src/ALOS_pre_process/lib_cpx.c
    src/ALOS_pre_process/lib_file.c
    src/ALOS_pre_process/lib_func.c
    src/ALOS_pre_process/put_sio_struct.c
    src/ALOS_pre_process/resamp.h
    src/ALOS_pre_process/resamp_azimuth.c
    )
target_include_directories(alos PUBLIC
    include
    src/ALOS_pre_process
    )
target_link_libraries(alos PUBLIC isce2::DataAccessorLib)

Python_add_library(cosar MODULE
    bindings/cosarmodule.cpp
    src/cosar/Header.cpp
    src/cosar/Burst.cpp
    src/cosar/Cosar.cpp
    )
target_include_directories(cosar PUBLIC
    include
    src/cosar
    )

InstallSameDir(${installfiles})
