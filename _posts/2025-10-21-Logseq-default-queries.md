---
layout: post
title:  "Logseq Default Queries"
date:   2025-10-21 19:00:00 +0100
tags: logseq, tech
---

I use logseq most days. It keeps my entire life in (something resembling) order. I rely on it quite heavily. I also find it quite fun.

To make it work for me I've set up several default queries. Default queries show their results at the bottom of today's journal page. You can add them by editting the `logseq/config.edn` file. Here's what I've got:

```
 ;; The following queries will be displayed at the bottom of today's journal page.
 ;; The "NOW" query returns tasks with "NOW" or "DOING" status.
 ;; The "NEXT" query returns tasks with "NOW", "LATER", or "TODO" status.
 :default-queries
 {:journals
  [
  
{:title "⚠️ Urgent"
 :query [:find (pull ?b [*])
        :where
        [?b :block/priority "A"]
        [?b :block/marker ?m]
        [(contains? #{"TODO" "DOING" "WAITING"} ?m)]]
   :group-by-page? false
   :breadcrumb-show? false
   }
   
   {:title "➡️ Next" 
  :query [[next]]
   :group-by-page? false
   :breadcrumb-show? false}
   
{:title "🎯 Big Important Stuff"
  :query [[important]]
   :group-by-page? false
   :breadcrumb-show? false}
   
  {:title "🔨 Work In Progress"
    :query [:find (pull ?h [*])
            :in $ ?start ?today
            :where
            [?h :block/marker ?marker]
            [(contains? #{"NOW" "DOING"} ?marker)]
            [?h :block/page ?p]
            [?p :block/journal? true]
            [?p :block/journal-day ?d]
            [(>= ?d ?start)]
            [(<= ?d ?today)]]
    :inputs [:30d :today]
    :group-by-page? false
    :breadcrumb-show? false
    }
    
      {:title "🕰️ Waiting"
    :query [:find (pull ?h [*])
            :in $ ?start ?today
            :where
            [?h :block/marker ?marker]
            [(contains? #{"WAITING"} ?marker)]
            [?h :block/page ?p]
            [?p :block/journal? true]
            [?p :block/journal-day ?d]
            [(>= ?d ?start)]
            [(<= ?d ?today)]]
    :inputs [:60d :today]
    :group-by-page? false
    :breadcrumb-show? false
    }

```

- For the "urgent" one I use the "priority" tag which logseq uses, you can activate "priority = A" for a block by typing "/A" and hitting enter.
- For "next" I actually tag things as "next" (I know this is confusing, because there's also a status called "NEXT", but I like using the TODO/DOING/DONE workflow instead.