# `node_type_from_graph()` works

    Code
      node_type_from_graph(graph)
    Output
                   tf_1              tf_2              tf_3              tf_4 
      "terminal parent"    "intermediate"    "intermediate"    "intermediate" 
                   tf_5              tf_6 
         "intermediate" "terminal parent" 

---

    Code
      node_type_from_graph(graph, drop = "tf_4")
    Output
                   tf_1              tf_2              tf_3              tf_5 
      "terminal parent"    "intermediate"    "intermediate"    "intermediate" 
                   tf_6 
      "terminal parent" 

# `dm_to_tibble()`/`tibble_to_dm()` round trip works

    Code
      tbl
    Output
      # A tibble: 5 x 6
        h     i     j        j1 tf_3$g $tf_2            tf_5            
        <chr> <chr> <chr> <int> <chr>  <nested>         <nested>        
      1 a     three C         3 two    <tibble [0 x 3]> <tibble [0 x 3]>
      2 b     four  D         4 three  <tibble [1 x 3]> <tibble [1 x 3]>
      3 c     five  E         5 four   <tibble [2 x 3]> <tibble [1 x 3]>
      4 d     six   F         6 five   <tibble [2 x 3]> <tibble [1 x 3]>
      5 e     seven F         6 five   <tibble [2 x 3]> <tibble [1 x 3]>

---

    Code
      tbl$tf_3$tf_2[[3]]
    Output
      # A tibble: 2 x 3
        c         d tf_1$b
        <chr> <int> <chr> 
      1 lion      3 C     
      2 dog       6 F     

---

    Code
      tbl$tf_5[[2]]
    Output
      # A tibble: 1 x 3
            k m     tf_6$o
        <int> <chr> <chr> 
      1     1 house e     

---

    Code
      dm2
    Output
      -- Metadata --------------------------------------------------------------------
      Tables: `tf_4`, `tf_5`, `tf_3`, `tf_6`, `tf_2`, `tf_1`
      Columns: 18
      Primary keys: 6
      Foreign keys: 5

---

    Code
      dm2$tf_4
    Output
      # A tibble: 5 x 4
        h     i     j        j1
        <chr> <chr> <chr> <int>
      1 a     three C         3
      2 b     four  D         4
      3 c     five  E         5
      4 d     six   F         6
      5 e     seven F         6

---

    Code
      dm2$tf_1
    Output
      # A tibble: 5 x 2
            a b    
        <int> <chr>
      1     2 B    
      2     3 C    
      3     6 F    
      4     4 D    
      5     7 G    

---

    Code
      dm2$tf_6
    Output
      # A tibble: 3 x 2
        n          o    
        <chr>      <chr>
      1 house      e    
      2 tree       f    
      3 streetlamp h    

---

    Code
      waldo::compare(dm_ptype(dm1), dm_ptype(dm2))
    Output
      `names(old)`: "tf_1" "tf_2" "tf_3" "tf_4" "tf_5" "tf_6"
      `names(new)`: "tf_4" "tf_5" "tf_3" "tf_6" "tf_2" "tf_1"
      
      `names(old$tf_2$data)`: "c" "d"  "e" "e1"
      `names(new$tf_2$data)`: "e" "e1" "c" "d" 
      
      `names(old$tf_3$fks)`: "tf_2" "tf_4"
      `names(new$tf_3$fks)`: "tf_4" "tf_2"
      
      `old$tf_4$fks$tf_5$on_delete`: "cascade"  
      `new$tf_4$fks$tf_5$on_delete`: "no_action"
      
      `names(old$tf_5$data)`: "k" "l" "m"
      `names(new$tf_5$data)`: "l" "k" "m"

# `dm_wrap()` and `dm_unwrap()` work

    Code
      dm_wrapped
    Output
      -- Metadata --------------------------------------------------------------------
      Tables: `tf_2`, `tf_3`, `tf_4`, `tf_5`, `tf_6`
      Columns: 17
      Primary keys: 5
      Foreign keys: 4

---

    Code
      dm_wrapped$tf_2
    Output
      # A tibble: 6 x 5
        c            d e        e1 tf_1$b
        <chr>    <int> <chr> <int> <chr> 
      1 elephant     2 D         4 B     
      2 lion         3 E         5 C     
      3 seal         4 F         6 D     
      4 worm         5 G         7 E     
      5 dog          6 E         5 F     
      6 cat          7 F         6 G     

---

    Code
      dm_unwrapped
    Output
      -- Metadata --------------------------------------------------------------------
      Tables: `tf_2`, `tf_3`, `tf_4`, `tf_5`, `tf_6`, `tf_1`
      Columns: 18
      Primary keys: 6
      Foreign keys: 5

---

    Code
      dm_unwrapped$tf_1
    Output
      # A tibble: 6 x 2
            a b    
        <int> <chr>
      1     2 B    
      2     3 C    
      3     4 D    
      4     5 E    
      5     6 F    
      6     7 G    

# `dm_pack_wrap()`, `dm_unpack_unwrap()`, `dm_nest_wrap()`, `dm_unnest_unwrap()` work

    Code
      dm_packed
    Output
      -- Metadata --------------------------------------------------------------------
      Tables: `tf_2`, `tf_3`, `tf_4`, `tf_5`, `tf_6`
      Columns: 17
      Primary keys: 5
      Foreign keys: 4

---

    Code
      dm_packed_nested
    Output
      -- Metadata --------------------------------------------------------------------
      Tables: `tf_3`, `tf_4`, `tf_5`, `tf_6`
      Columns: 13
      Primary keys: 4
      Foreign keys: 3

---

    Code
      dm_packed_nested_unnested
    Output
      -- Metadata --------------------------------------------------------------------
      Tables: `tf_3`, `tf_4`, `tf_5`, `tf_6`, `tf_2`
      Columns: 17
      Primary keys: 5
      Foreign keys: 4

---

    Code
      dm_packed_nested_unnested_unpacked
    Output
      -- Metadata --------------------------------------------------------------------
      Tables: `tf_3`, `tf_4`, `tf_5`, `tf_6`, `tf_2`, `tf_1`
      Columns: 18
      Primary keys: 6
      Foreign keys: 5
