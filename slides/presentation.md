# Clojure Gems
## Hidden Beauties in Clojure

Alex Robbins &nbsp;&nbsp;&nbsp;&nbsp; ![factual-logo]

---

# Clojure is wonderful

There are some extra-wonderful functions/features that you might not know about. You can get by without these functions, but with them you'll be happier.

---

# Data structures are their own best functions!

```clojure
(map {:a 1 :b 2} [:a :c])
;; (1 nil)

(map #{:a} [:a :b])
;; (:a nil)

([:a :b] 0)
;; :a
```
---

# Destructuring

```clojure
(def input [1 {:key "value" :key2 "value2"}])

(let [[a] input]
  a)
  ;; 1

(let [[_ a] input]
  a)
  ;; {:key "value" :key2 "value"}

(let [[_ {a :key}] input]
  a)
  ;; "value"

(let [[_ {:keys [:key :key2] :as whole-map}] input]
  [key key2 whole-map])
  ;; ["value" "value2" {:key "value" :key2 "value2"}]
```
---

# zero? pos? neg?
# even? odd?

```clojure
(map zero? [0 1])
;; (true false)

(map pos? [0 1])
;; (false true)
```
---

# not=
## No more #(not (= %1 %2))

```
(not= 0 1)
;; true
```
---

# compare
## General purpose greater-than

```
(compare 0 1)
;; -1
(compare "b" "a")
;; 1
(compare :a :a)
;; 0
```
---

# for
## :let :while :when

```
(for [x (range)
      :let [x2 (* x x)]
      :when (odd? x)
      :while (< x2 100)]
     [x x2])
;; ([1 1] [3 9] [5 25] [7 49] [9 81])
```
---

# mapcat
## (apply concat (map f s))

```
(mapcat (fn [x] [x (* x x)]) [0 1 2])
;; (0 0 1 1 2 4)

(mapcat expand-variant-spellings ["Alexander" "John"])
["Alexander" "Aleksander" "Alex" "John" "Jon"]
```
---

# zipmap
## Make a map from keyseq and valseq
```
(zipmap [:a :b :c] (range))
;; {:c 2, :b 1, :a 0}
```
---

# pmap
## Run map in parallel

```
(pmap inc (range 100000000))
;; same as (map inc (range 100000000)), but computed on all cores
```
---

# reductions
## freeze-frame for reduce

```
(reductions + [1 1 1 1 1])
;; (1 2 3 4 5)

(reductions conj [] [1 2 3])
;; ([] [1] [1 2] [1 2 3])
```
---

# condp
## Great function, crazy doc string

```
(condp = (:type {:type :person :name "Alex"})
  :person (println "Person found")
  :canine (println "Dog found"))
```
---

# group-by
## A personal favorite!

```
(group-by :suspicious [{:name "Alex"  :suspicious false}
                       {:name "Chris" :suspicious true}
                       {:name "Lee"   :suspicious false}])
;; {false [{:suspicious false, :name "Alex"}
           {:suspicious false, :name "Lee"}],
    true  [{:suspicious true,  :name "Chris"}]}
```
---

# get-in
## Reach into nested maps
```
(get-in {:a {:b 1}} [:a :b])
;; 1
```
---

# constantly
## Make a constant function
```
(map (constantly 1) [1 2 3 4])
;; (1 1 1 1)
```

---

# fnil
## Automatic nil checks
```
(def nil-patched-+ (fnil + 1))
(nil-patched-+ nil 2)
;; 3
```
---

# Clojure Gems
## Hidden Beauties in Clojure

Alex Robbins

- alexr@factual.com &nbsp;&nbsp;&nbsp;&nbsp; ![factual-logo]
- alexander.j.robbins@gmail.com
- https://github.com/alexrobbins/clojure-gems

Factual is hiring!

[factual-logo]: images/factual-high-res.png "Factual"
