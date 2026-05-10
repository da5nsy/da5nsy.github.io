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
   
         {
      ;; copied from: https://github.com/YU000jp/Logseq-default-queries-journals
    ;; Advanced query: Find scheduled tasks for next 14 days 
    ;; Useful for planning and calendar view
    :title "⏰ TODOs scheduled in the next 10 days"
    :query [:find (pull ?block [*])        ;; Pull all block properties
            :in $ ?start ?next             ;; Input parameters: start and next 14 days
            :where
            [?block :block/marker ?marker]  ;; Find blocks with task markers
            [?block :block/scheduled ?d]   ;; Only check scheduled date
            [(> ?d ?start)]                ;; Date > start date (today)
            [(< ?d ?next)]                 ;; Date < end date (14 days from now)
            [(contains? #{"TODO"} ?marker)] ;; Only show TODO tasks
    ]
    :inputs [:0d :14d-after]              ;; Set date range: today to 14 days ahead
    :result-transform (fn [result]         ;; Sort results by scheduled date
                       (sort-by (juxt (fn [d] (get d :block/scheduled)) result))
                       (sort-by (fn [d]
                                  (get d :block/scheduled)) result))
    :collapsed? false
    :breadcrumb-show? false
  }
  
    {
    ;; copied from: https://github.com/YU000jp/Logseq-default-queries-journals
    ;; Advanced query: Show tasks due within next 10 days
    :title "📆 TODOs with deadlines in the next 10 days"
    :query [:find (pull ?block [*])
            :in $ ?start ?next       ;; Input parameters: start and end dates
            :where
            [?block :block/marker ?marker]
            [?block :block/deadline ?d]  ;; Only check deadline
            [(> ?d ?start)]                ;; Date > start date
            [(< ?d ?next)]                 ;; Date < end date (10 days from now)
            [(contains? #{"TODO"} ?marker)] ;; Only TODO tasks
    ]
    :inputs [:0d :10d-after]
    :result-transform (fn [result]
                       (sort-by (juxt (fn [d] (get d :block/deadline)) result))
                       (sort-by (fn [h]
                                  (get h :block/deadline)) result))
    :collapsed? false
    :breadcrumb-show? false
  }
   
	{:title "🎯 Big Important Stuff"
	 :query (and [[important]] (or (task TODO) (task DOING) (task WAITING)))
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
	:collapsed? false
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
	:collapsed? false
    }
    
   {:title "📅 NEXT"
    :query [:find (pull ?h [*])
            :in $ ?start ?next
            :where
            [?h :block/marker ?marker]
            [(contains? #{"NOW" "LATER" "TODO"} ?marker)]
            [?h :block/page ?p]
            [?p :block/journal? true]
            [?p :block/journal-day ?d]
            [(> ?d ?start)]
            [(< ?d ?next)]]
    :inputs [:today :7d-after]
    :group-by-page? false
    :breadcrumb-show? false
    }
   
  
    ]}

```

- For the "urgent" one I use the "priority" tag which logseq uses, you can activate "priority = A" for a block by typing "/A" and hitting enter.
- For "next" I actually tag things as "next" (I know this is confusing, because there's also a status called "NEXT", but I like using the TODO/DOING/DONE workflow instead.