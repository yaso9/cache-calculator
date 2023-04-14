<script lang="ts">
  let A: number;
  let B: number;
  let C: number;
  let S: number;
  let m: number;
  let b: number;
  let s: number;
  let t: number;
  let addrHex: string;
  let blockOffset: string;
  let setIndex: string;
  let tag: string;

  $: {
    S = C / (A * B)
    b = Math.log2(B)
    s = Math.log2(S)
    t = m - b - s
    const addr = parseInt(addrHex, 16)
    blockOffset = (addr & ((1 << b) - 1)).toString(16)
    setIndex = ((addr >> b) & ((1 << s) - 1)).toString(16)
    tag = (addr >> (b + s)).toString(16)
  }
</script>


<div class="container">
  <div class="row my-4">
      <div class="card col-6 offset-3">
        <div class="card-body">
          <h1>The Cool Kids' CPU Cache Calculator</h1>
          <div class="alert alert-primary" role="alert">
            Recall, direct mapped means A = 1, fully associative means S = 1, and set associative means everything else. The notation we use is $(A, B, C).
          </div>
          <div class="mb-3">
            <label for="A" class="form-label">A (associativity)</label>
            <input type="number" class="form-control" id="A" bind:value={A}/>
          </div>
          <div class="mb-3">
            <label for="B" class="form-label">B (bytes per block or line)</label>
            <input type="number" class="form-control" id="B" bind:value={B}/>
          </div>
          <div class="mb-3">
            <label for="C" class="form-label">C (capacity)</label>
            <input type="number" class="form-control" id="C" bind:value={C}/>
          </div>
          <div class="mb-3">
            <label for="S" class="form-label">S (# sets) = C / (A * B)</label>
            <input type="number" class="form-control" id="S" bind:value={S} disabled/>
          </div>
          <div class="mb-3">
            <label for="m" class="form-label">M (address width in bits)</label>
            <input type="number" class="form-control" id="m" bind:value={m}/>
          </div>
          <div class="mb-3">
            <label for="b" class="form-label">b (# block offset bits) = log(B)</label>
            <input type="number" class="form-control" id="b" bind:value={b} disabled/>
          </div>
          <div class="mb-3">
            <label for="s" class="form-label">s (# set index bits) = log(S)</label>
            <input type="number" class="form-control" id="s" bind:value={s} disabled/>
          </div>
          <div class="mb-3">
            <label for="t" class="form-label">t (# tag bits) = m - b - s</label>
            <input type="number" class="form-control" id="t" bind:value={t} disabled/>
          </div>
          <div class="mb-3">
            <label for="address" class="form-label">Address (hex)</label>
            <div class="input-group">
              <span class="input-group-text">0x</span>
              <input type="text" class="form-control" id="address" bind:value={addrHex}/>
            </div>
          </div>
          <div class="input-group mb-3">
            <label for="blockOffset" class="form-label">Block Offset</label>
            <div class="input-group">
              <span class="input-group-text">0x</span>
              <input type="text" class="form-control" id="blockOffset" bind:value={blockOffset} disabled/>
            </div>
          </div>
          <div class="input-group mb-3">
            <label for="setIndex" class="form-label">Set Index</label>
            <div class="input-group">
              <span class="input-group-text">0x</span>
              <input type="text" class="form-control" id="tag" bind:value={setIndex} disabled/>
            </div>
          </div>
          <div class="input-group mb-3">
            <label for="tag" class="form-label">Tag</label>
            <div class="input-group">
              <span class="input-group-text">0x</span>
              <input type="text" class="form-control" id="tag" bind:value={tag} disabled/>
            </div>
          </div>
        </div>
      </div>
  </div>
</div>
