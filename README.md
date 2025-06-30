```bash
#!/bin/bash

# Function to display the table
generate_table() {
  local number=$1
  local start=$2
  local end=$3
  local order=$4
  local loop_type=$5

  echo
  echo "Multiplication table for $number from $start to $end ($order order, $loop_type loop):"

  if [ "$order" == "asc" ]; then
    if [ "$loop_type" == "list" ]; then
      for i in $(seq $start $end); do
        echo "$number x $i = $((number * i))"
      done
    else
      for ((i=start; i<=end; i++)); do
        echo "$number x $i = $((number * i))"
      done
    fi
  else
    if [ "$loop_type" == "list" ]; then
      for i in $(seq $end -1 $start); do
        echo "$number x $i = $((number * i))"
      done
    else
      for ((i=end; i>=start; i--)); do
        echo "$number x $i = $((number * i))"
      done
    fi
  fi
}

while true; do
  echo -n "Enter a number for the multiplication table: "
  read number

  # Check if number is an integer
  if ! [[ "$number" =~ ^[0-9]+$ ]]; then
    echo "Invalid number. Please enter a valid integer."
    continue
  fi

  echo -n "Do you want a full table or partial? (f/p): "
  read table_type

  if [ "$table_type" == "p" ]; then
    echo -n "Enter starting number (1–10): "
    read start
    echo -n "Enter ending number (1–10): "
    read end

    if ! [[ "$start" =~ ^[0-9]+$ && "$end" =~ ^[0-9]+$ && $start -le $end && $start -ge 1 && $end -le 10 ]]; then
      echo "Invalid range. Showing full table instead."
      start=1
      end=10
    fi
  else
    start=1
    end=10
  fi

  echo -n "Choose loop type - list or c-style? (list/c): "
  read loop_type
  if [ "$loop_type" != "c" ]; then
    loop_type="list"
  fi

  echo -n "Do you want ascending or descending order? (asc/desc): "
  read order
  if [ "$order" != "desc" ]; then
    order="asc"
  fi

  generate_table "$number" "$start" "$end" "$order" "$loop_type"

  echo
  echo -n "Do you want to try another number? (y/n): "
  read again
  if [ "$again" != "y" ]; then
    echo "Goodbye!"
    break
  fi
done
```
``

🧪 How to Run

Save it as multiplication_table.sh, make it executable and run:

chmod +x multiplication_table.sh
./multiplication_table.sh
