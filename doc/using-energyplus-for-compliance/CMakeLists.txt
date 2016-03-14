
# to get the list of input files, go to the root of the document folder, and:
# grep -r '\\input{' * | cut -d ':' -f 2 | cut -c 8- | rev | cut -c 2- | rev | sed 's|^|  ${CMAKE_SOURCE_DIR}/doc/acknowledgements/|g' | sed 's/$/.tex/g' 
SET( INCLUDED_TEX
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/../title.tex
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/../header.tex
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/src/using-energyplus-for-compliance.tex
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/src/introduction.tex
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/src/introduction/background.tex
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/src/introduction/compliance-objects.tex
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/src/introduction/tabular-summary-reports.tex
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/src/introduction/features-related-to-appendix-g-and-leed.tex
  ${CMAKE_SOURCE_DIR}/doc/using-energyplus-for-compliance/src/introduction/features-related-to-california-title-24.tex
)

# to get the list of inluded images, go to the root of the document folder and:
# grep -r '\\includegraphics' * | cut -d ':' -f 2 | rev | cut -d '{' -f 1 | rev | cut -d '}' -f 1 | sed 's/^/  /g' | sort -n -t'.' -k 1.14
SET( INCLUDED_IMAGES 
) 

SET( SOURCE_FILENAME "using-energyplus-for-compliance" )
SET( OUTPUT_FILENAME "UsingEnergyPlusForCompliance" )

add_custom_command( OUTPUT ${CMAKE_BINARY_DIR}/doc-build/${OUTPUT_FILENAME}.pdf
                    COMMAND ${CMAKE_COMMAND} -DXELATEX=${XELATEX} -DINNAME=${SOURCE_FILENAME} -DOUTNAME=${OUTPUT_FILENAME} -P ${CMAKE_SOURCE_DIR}/cmake/BuildDocumentation.cmake
		    WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/doc-build/${SOURCE_FILENAME}
		    DEPENDS ${INCLUDED_TEX} ${INCLUDED_IMAGES}
                 ) 
add_custom_target( zPDF_${OUTPUT_FILENAME} ALL
                   DEPENDS ${CMAKE_BINARY_DIR}/doc-build/${OUTPUT_FILENAME}.pdf
                 )