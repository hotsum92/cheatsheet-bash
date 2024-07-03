```
gnuplot --persist -e 'plot sin(x)'
```

```
echo -e "1 2 3\n2 3 4\n3 4 5" | \
gnuplot --persist -e 'plot "-" using 1:2 with lines'

echo -e "1 2 3\n2 3 4\n3 4 5" | \
gnuplot --persist -e 'plot "-" with points'
```

```
src=$(cat << 'EOF'
plot "-" using 1:2 with lines,
     "-" using 1:3 with lines;
EOF
)
echo -e "1 2 3\n2 3 4\n3 4 5\ne\n1 2 3\n2 3 4\n3 4 5" | \
gnuplot -p -e "$src"

src=$(cat << 'EOF'
plot for [i=2:*] "-" using 1:i with lines;
EOF
)
echo -e "1 2 3\n2 3 4\n3 4 5\ne\n1 2 3\n2 3 4\n3 4 5" | \
gnuplot -p -e "$src"

```

```
gnuplot << EOF
set terminal png
set output "sin.png"
plot sin(x)
EOF
```

```

gnuplot << EOF
set terminal png
set output "output.png"
set style data linespoints
set datafile separator ","
set xdata time
set timefmt "%b %d %H:%M:%S GMT %Y"
set xlabel "timestamp"
set ylabel "percent"
plot "data.csv" using 1:3 title "a","data.csv" using 1:4 title "b"
EOF

```

```

gnuplot --persist << EOF
set style data linespoints
set datafile separator ","
set xdata time
set timefmt "%b %d %H:%M:%S GMT %Y"
set xlabel "timestamp"
set ylabel "percent"
plot "data.csv" using 1:3 title "A","data.csv" using 1:4 title "B"
EOF

```

```
tmpfile=$(mktemp)

cat - | awk '{print NR, $0}' > $tmpfile

gnuplot --persist -e "plot for [i=3:*] \"$tmpfile\" using 1:i:xtic(2) title columnheader(i) with linespoints" 2>/dev/null
```
