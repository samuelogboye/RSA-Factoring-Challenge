#!/usr/bin/env bash
# This is a factors challenge

check_factor() {
    if [ $# -ne 1 ]; then
        echo "Usage: check_factor <number>"
        exit 1
    fi

    factors=$(factor "$1" | awk '{$1=""; print $0}' | sed 's/ //g')
    factors_array=($factors)

    if [ ${#factors_array[@]} -eq 1 ]; then
        echo "$1=1*$1"
    else
        max_factor=${factors_array[-1]}
        second_max_factor=${factors_array[-2]}

        if [ ${#factors_array[@]} -gt 2 ]; then
            for ((i=${#factors_array[@]}-3; i>=0; i--)); do
                if [ $(echo "${factors_array[$i]}*$second_max_factor" | bc) -gt $(echo "$max_factor*${
factors_array[$i+1]}" | bc) ]; then
                    break
                fi

                second_max_factor=${factors_array[$i]}
            done
        fi

        echo "$1=$max_factor*$second_max_factor"
    fi
}

if [ $# -ne 1 ]; then
    echo 'Usage: factors <file>'
    exit 1
else
    while read -r number; do
        check_factor "$number"
    done < "$1"
fi
