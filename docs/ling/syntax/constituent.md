# Constituents & Categories

## Lexical / Functional Category

Lexical categories (实词):

* open in membership, 实词的总量可能增减
* do not vary greatly across languages
* typically contentful
* (at least) one of the syllables is frequently stressed

<!-- the study of lexical categories concentrate on 4 categories of words, divided according to their binary features [N] and [V]

* N. 名词：[+N, -V]
* V. 动词：[-N, +V]
* Adj. 形容词：[+N, +V]
* P. 介词：[-N, -V]

> 英语的介词和汉语的不太一样，是有实际意义的，算作实词 -->

Functional category (虚词): including determiner (D), demonstrative, Num, mood, tense (T), aspect (Asp.), agreement (Agr.，person + gender + number), complementizer (C) ...

* closed in membership
* semantically abstract, denoting mostly grammatical functions
* vary a lot across languages
* unstressed phonologically

## Diagnotics for Categories

Diagnotics 的意思是用随便什么方法，包括肉眼观察，对随便什么语料作出随便高层次还是低层次的语法上的判断。比如说判断一个成分的类别（名词短语？动词短语？……），比如说修改“病”句（中英文都用了“看病”的隐喻，真有意思）

判断类别的标准：

* morphological criteria: inflection / derivational morphemes
* syntactic criteria: guess the word category from the categories of its context
* phonological criteria: 'increase', 'servey', 'record', which syllable is stressed?
* semantic criteria: 根据语义来猜一个词是什么词类，虽然很符合直觉但不一定准，比如日语里用来表示形容语义的词类有“形容动词”这种妖孽

## Constituent Structure

Tree Diagram terminologies:

* root (根节点) / terminal (相当于数据结构上说的叶子节点) / non-terminal nodes (neither root nor terminal)
* branch: each single line in a tree diagram
* mother / daughter / grand daughter /sister node
* dominance / constituency: if there exists a continuous decending path from a higher node to a lower one, then we say the higher one dominates the lower one, and the lower one is a constituent of the higher one
* immediate dominance: no other nodes intervenes the higher and lower nodes, e.g. a pair of mother and daughter node

为了方便排版，句法树还可以写成下面这种一维的表示；[jsSyntaxTree](https://ironcreek.net/syntaxtree/) 可以通过这种一维的表示画出树形图

$$
[_{S}[_{NP1}[_{N1}Boris]][_{VP}[_{V}talked][_{PP1}[_{P1}to][_{NP2}[_{D}the][_{N}reporter]]][_{PP2}[_{P2}about][_{NP3}[_{Pronoun}himself]]]]]
$$

It is not good to use ternary or more complex branch in tree diagrams. We will learn advanced mothods (X-bar theory) to avoid ternary branches in the future.

## Constituency Test

不管以后学到什么高深的句法理论，constituency test 永远是判断短语成分的层次关系的唯一标准

* movement (permutation): Only constituents can be moved as a single unit.
    * wh-test，英语允许用 wh- 开头的特殊疑问词对成分提问。Movement leaves a silent copy, previously called trace (t, 语迹), in the original place. e.g. To whom did the party chairman send a book _t_?
    * topicalization: The fronting of a sentence-internal phrase to the beginning of the sentences. e.g. The new car, Mary hopes that John will like _t_.
    * clefting: the permutation of the order of elements，在英语里就是用 it 形式主语来改语序
* substitution (pronomialization): a pronoun substitutes a entire phrase. e.g. [He] has done [so] too. I 和 so 都是代词，分别代替 NP 和 VP
* deletion (ellipsis): e.g. John can [do sth] and Mary can too.
* conjunction: only constituents of the same type can be coordinated
* fragments: a constituent can serve as a short answer to questions.

Failing in a test does not mean a fragment is not a constituent, but passing a test means the opposite. e.g. - What has the president done? - Has resigned. (The answer is syntactically wrong! It should be "Resigned.", but "has resigned" __is__ a constituent.)

Recoverablity condition: substitution 和 ellipsis 的时候，要求产生的新句子在语义上可以看出什么成分被替换 / 删除了
