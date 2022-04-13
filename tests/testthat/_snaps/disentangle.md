# dm_disentangle() works

    Code
      dm_disentangle(dm_for_filter_w_cycle(), tf_1) %>% dm_get_all_fks()
    Output
      # A tibble: 11 x 5
         child_table child_fk_cols parent_table parent_key_cols on_delete
         <chr>       <keys>        <chr>        <keys>          <chr>    
       1 tf_2        d             tf_1         a               no_action
       2 tf_7-2      q             tf_2         c               no_action
       3 tf_5-1      l             tf_4-1       h               cascade  
       4 tf_5-1      m             tf_6-1       n               no_action
       5 tf_6-2      o             tf_7-2       p               no_action
       6 tf_5-2      m             tf_6-2       n               no_action
       7 tf_5-2      l             tf_4-2       h               cascade  
       8 tf_2        e, e1         tf_3-1       f, f1           no_action
       9 tf_4-1      j, j1         tf_3-1       f, f1           no_action
      10 tf_6-1      o             tf_7-1       p               no_action
      11 tf_4-2      j, j1         tf_3-2       f, f1           no_action
    Code
      dm_disentangle(dm_for_filter_w_cycle(), tf_5) %>% dm_get_all_fks()
    Output
      # A tibble: 12 x 5
         child_table child_fk_cols parent_table parent_key_cols on_delete
         <chr>       <keys>        <chr>        <keys>          <chr>    
       1 tf_5        l             tf_4-1       h               cascade  
       2 tf_7-1      q             tf_2-1       c               no_action
       3 tf_6-1      o             tf_7-1       p               no_action
       4 tf_5        m             tf_6-2       n               no_action
       5 tf_6-2      o             tf_7-2       p               no_action
       6 tf_7-2      q             tf_2-2       c               no_action
       7 tf_4-1      j, j1         tf_3-1       f, f1           no_action
       8 tf_2-1      e, e1         tf_3-1       f, f1           no_action
       9 tf_2-1      d             tf_1-1       a               no_action
      10 tf_2-2      d             tf_1-2       a               no_action
      11 tf_2-2      e, e1         tf_3-2       f, f1           no_action
      12 tf_4-2      j, j1         tf_3-2       f, f1           no_action
    Code
      dm_disentangle(entangled_dm(), a) %>% dm_get_all_fks()
    Output
      # A tibble: 22 x 5
         child_table child_fk_cols parent_table parent_key_cols on_delete
         <chr>       <keys>        <chr>        <keys>          <chr>    
       1 a           a             b-1          b               no_action
       2 b-1         b             d-1          d               no_action
       3 c-1         c             d-1          d               no_action
       4 d-1         d             e-1          e               no_action
       5 e-1         e             g-1          g               no_action
       6 f-1         f             g-1          g               no_action
       7 d-1         d             f-2          f               no_action
       8 f-2         f             g-2          g               no_action
       9 e-2         e             g-2          g               no_action
      10 a           a             c-2          c               no_action
      # ... with 12 more rows
    Code
      dm_disentangle(entangled_dm(), c) %>% dm_get_all_fks()
    Output
      # A tibble: 22 x 5
         child_table child_fk_cols parent_table parent_key_cols on_delete
         <chr>       <keys>        <chr>        <keys>          <chr>    
       1 a-2         a             c            c               no_action
       2 c           c             d-1          d               no_action
       3 b-1         b             d-1          d               no_action
       4 d-1         d             e-1          e               no_action
       5 e-1         e             g-1          g               no_action
       6 f-1         f             g-1          g               no_action
       7 d-1         d             f-2          f               no_action
       8 f-2         f             g-2          g               no_action
       9 e-2         e             g-2          g               no_action
      10 a-1         a             b-1          b               no_action
      # ... with 12 more rows
    Code
      dm_disentangle(entangled_dm_2(), a) %>% dm_get_all_fks()
    Output
      # A tibble: 8 x 5
        child_table child_fk_cols parent_table parent_key_cols on_delete
        <chr>       <keys>        <chr>        <keys>          <chr>    
      1 a           a             d-1          d               no_action
      2 b-1         b             d-1          d               no_action
      3 c-1         c             d-1          d               no_action
      4 b-2         b             d-2          d               no_action
      5 c-2         c             d-2          d               no_action
      6 d-1         d             e-1          e               no_action
      7 a           a             e-2          e               no_action
      8 d-2         d             e-2          e               no_action
    Code
      dm_disentangle(entangled_dm_2(), d) %>% dm_get_all_fks()
    Output
      # A tibble: 6 x 5
        child_table child_fk_cols parent_table parent_key_cols on_delete
        <chr>       <keys>        <chr>        <keys>          <chr>    
      1 b           b             d            d               no_action
      2 c           c             d            d               no_action
      3 a-2         a             d            d               no_action
      4 d           d             e-1          e               no_action
      5 a-1         a             e-1          e               no_action
      6 a-2         a             e-2          e               no_action
