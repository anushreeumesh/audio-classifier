CHANGE VALIDATE OR TEST depending
RUN THIS IN THE SPECTROGRAM FOLDER 

cd YOUR DATA SET IMAGE FOLDER FILE PATH
vi convert_to_lst.sh

PASTE THIS CONTENT:########################
#!/bin/bash
A_file_path="validate/eastern-whipbird"
A_identifier="0"
B_file_path="validate/kookaburra"
B_identifier="1"
C_file_path="validate/superb-lyrebird"
C_identifier="2"
D_file_path="validate/willie-wagtail"
D_identifier="3"

output_file_name="bird-audio-validate.lst"

## output identifier and file name then append to same file, make the index last

declare -a array

A_file_list=$(find $A_file_path -type f | rev | cut -d'/' -f-2 | rev | sort -n)

for A_file_name in $A_file_list;
do
 array+=("$A_identifier $A_file_name")
done

B_file_list=$(find $B_file_path -type f | rev | cut -d'/' -f-2 | rev | sort -n)

for B_file_name in $B_file_list;
do
 array+=("$B_identifier $B_file_name")
done

C_file_list=$(find $C_file_path -type f | rev | cut -d'/' -f-2 | rev | sort -n)

for C_file_name in $C_file_list;
do
 array+=("$C_identifier $C_file_name")
done

D_file_list=$(find $D_file_path -type f | rev | cut -d'/' -f-2 | rev | sort -n)

for D_file_name in $D_file_list;
do
 array+=("$D_identifier $D_file_name")
done

# prints array one element per line
#printf '%s\n' "${array[@]}"

## add an index key at the beginning over every element of output and write to newfile

len=${#array[@]}
i=0
while [ $i -lt $len ]; do
    echo "$i ${array[$i]}"
    let i++
done | tr [:blank:] \\t > $output_file_name
##########################