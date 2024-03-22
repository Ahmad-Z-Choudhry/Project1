# Project Analysis: Proof of Work Efficiency

## Experiment Results

- **Name:** Ahmad Choudhry

### Difficulty Levels and Results

- **k=2:**
  - **xs:** `1115009823this_is_a_bitcoin_block_of_68482271`
  - **Hash Value:** `00c6d3bbbeb11a2b00004194d4490b5d1646865fc6faf00266899e85cf419f2e`
  - **Time elapsed:** 1s
  - **number of trials:** 200

- **k=3:**
  - **xs:** `1335379180this_is_a_bitcoin_block_of_68482271`
  - **Hash Value:** `000e6f89b89a4105261daf9352af8b00f4601dc820693e0f7b5723d64bd121c2`
  - **Time elapsed:** 1s
  - **number of trials:** 10000

- **k=4:**
  - **xs:** `1115009823this_is_a_bitcoin_block_of_68482271`
  - **Hash Value:** `00c6d3bbbeb11a2b00004194d4490b5d1646865fc6faf00266899e85cf419f2e`
  - **Time elapsed:** 1s
  - **number of trials:** 1000000

- **k=5:**
  - **xs:** `1115009823this_is_a_bitcoin_block_of_68482271`
  - **Hash Value:** `00c6d3bbbeb11a2b00004194d4490b5d1646865fc6faf00266899e85cf419f2e`
  - **Time elapsed:** 1s
  - **number of trials:** 1000000

- **k=6:**
  - **xs:** `1115009823this_is_a_bitcoin_block_of_68482271`
  - **Hash Value:** `00c6d3bbbeb11a2b00004194d4490b5d1646865fc6faf00266899e85cf419f2e`
  - **Time elapsed:** 1s
  - **number of trials:** 1000000

- **k=7(Ran on GCP):**
  - **xs:** `950424022this_is_a_bitcoin_block_of_68482271`
  - **Hash Value:** `0000000d1e952d576b427b46df23e69f47c5b0209d0ede795777d50cfe9fe2fb`
  - **Time elapsed:** 354s
  - **number of trials:** 100000000

 To estimate the number of trials needed to find a nonce for a given difficulty (`k`), I used a combination of theoretical probability calculations and empirical adjustments based on computational capabilities. The process involves:

1. **Understanding Difficulty:** The difficulty (`k`) dictates the number of leading zeros required in the hash, influencing the probability of finding a matching hash.

2. **Calculating Probability:** The probability of success per trial is `1/16^k`, given the hexadecimal nature of hashes.

3. **Estimating Trials:** The expected number of trials is approximately the reciprocal of the success probability, suggesting `16^7` trials for `k=7`.

4. **Adjusting for Resources:** Actual computational power and parallelization capabilities significantly affect the speed and efficiency of trial executions.

5. **Empirical Testing:** Conducting smaller scale tests to refine estimates based on real-world performance and adjusting for practical factors like network latency in distributed systems.

6. **External Factors:** Consideration of factors like network hash rate and difficulty adjustments over time, if applicable.

For `k=7`, the estimation led to setting a target of 100,000,000 trials, based on both the calculated probability and adjustments for my specific computational setup and initial empirical findings.


### Configuration

- **Infrastructure:** Single Node (1 master, 0 workers)
- **Machine Type:** n2-standard-4
- **Number of GPUs:** 0

## Discussion on Efficiency

### Randomized Approach

**Pros:**
- **Diversity:** Random selection might stumble upon a valid nonce faster in some cases, especially if the valid nonces are unevenly distributed.
- **Parallelization:** It works well with distributed computing since each node can generate random nonces independently without worrying about duplicating work.

**Cons:**
- **Redundancy:** There's a chance of generating the same nonce multiple times, especially with a large number of trials, leading to wasted computations.
- **Unpredictability:** It's less systematic, making performance analysis and predictions more difficult.

### Sequential Approach

**Pros:**
- **Systematic:** Every possible nonce value within the range is guaranteed to be checked exactly once, eliminating redundancy.
- **Predictability:** It's easier to estimate the time to find a nonce since the approach is linear and methodical.

**Cons:**
- **Parallelization Issues:** Care must be taken to avoid overlap in nonce values when distributing the work across multiple nodes, which can complicate the implementation.
- **Potentially Slower:** If valid nonces are rare and located towards the end of the range, it might take longer to find one compared to randomly encountering it early on.

