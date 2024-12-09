<script lang="ts">
  import { Button, Card, Range } from 'flowbite-svelte'
  
  let bottomHoleTemp = 600
  let flow = 500
  let mudWeight = 16
  let viscosity = 40

  $: maxWorkingPressure = 3600
  $: differentialAdjustment = "-2% – 4%"
  $: estimatedPressure = "3600 – 3800"
  $: availableDiff = 0

  function handleGeneratePDF() {
    console.log('Generating PDF...')
  }
</script>

<div class="min-h-screen bg-gray-900 p-6">
  <div class="max-w-6xl mx-auto">
    <!-- Header -->
    <div class="flex justify-between items-start mb-6">
      <h1 class="text-white text-2xl font-semibold">Off-Bottom Pressure & Derating Recommendations</h1>
      <button class="text-gray-400 hover:text-white">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <!-- Left Panel -->
      <div class="lg:col-span-2">
        <Card class="bg-gray-800 border-gray-700">
          <div class="space-y-6">
            <!-- Bottom Hole Temperature -->
            <div>
              <label class="block text-sm font-medium text-gray-300 mb-2">
                Expected Bottom Hole Temperature
              </label>
              <div class="flex items-center gap-4">
                <Button size="xs" class="px-2" on:click={() => bottomHoleTemp = Math.max(0, bottomHoleTemp - 1)}>-</Button>
                <input
                  type="number"
                  bind:value={bottomHoleTemp}
                  class="bg-gray-700 border-gray-600 text-white text-center w-24 rounded-lg"
                />
                <Button size="xs" class="px-2" on:click={() => bottomHoleTemp = Math.min(1000, bottomHoleTemp + 1)}>+</Button>
              </div>
              <Range class="mt-2" min={0} max={1000} bind:value={bottomHoleTemp} />
              <div class="flex justify-between text-xs text-gray-400 mt-1">
                <span>0</span>
                <span>600</span>
                <span>1000</span>
              </div>
            </div>

            <!-- Flow -->
            <div>
              <label class="block text-sm font-medium text-gray-300 mb-2">
                Flow (GPM)
              </label>
              <div class="flex items-center gap-4">
                <Button size="xs" class="px-2" on:click={() => flow = Math.max(0, flow - 1)}>-</Button>
                <input
                  type="number"
                  bind:value={flow}
                  class="bg-gray-700 border-gray-600 text-white text-center w-24 rounded-lg"
                />
                <Button size="xs" class="px-2" on:click={() => flow = Math.min(2000, flow + 1)}>+</Button>
              </div>
              <Range class="mt-2" min={0} max={2000} bind:value={flow} />
              <div class="flex justify-between text-xs text-gray-400 mt-1">
                <span>0</span>
                <span>500</span>
                <span>2000</span>
              </div>
            </div>

            <!-- Mud Weight -->
            <div>
              <label class="block text-sm font-medium text-gray-300 mb-2">
                Mud Weight (GPM)
              </label>
              <div class="flex items-center gap-4">
                <Button size="xs" class="px-2" on:click={() => mudWeight = Math.max(0, mudWeight - 1)}>-</Button>
                <input
                  type="number"
                  bind:value={mudWeight}
                  class="bg-gray-700 border-gray-600 text-white text-center w-24 rounded-lg"
                />
                <Button size="xs" class="px-2" on:click={() => mudWeight = Math.min(25, mudWeight + 1)}>+</Button>
              </div>
              <Range class="mt-2" min={0} max={25} bind:value={mudWeight} />
              <div class="flex justify-between text-xs text-gray-400 mt-1">
                <span>0</span>
                <span>16</span>
                <span>25</span>
              </div>
            </div>

            <!-- Viscosity -->
            <div>
              <label class="block text-sm font-medium text-gray-300 mb-2">
                Viscosity (cP)
              </label>
              <div class="flex items-center gap-4">
                <Button size="xs" class="px-2" on:click={() => viscosity = Math.max(0, viscosity - 1)}>-</Button>
                <input
                  type="number"
                  bind:value={viscosity}
                  class="bg-gray-700 border-gray-600 text-white text-center w-24 rounded-lg"
                />
                <Button size="xs" class="px-2" on:click={() => viscosity = Math.min(100, viscosity + 1)}>+</Button>
              </div>
              <Range class="mt-2" min={0} max={100} bind:value={viscosity} />
              <div class="flex justify-between text-xs text-gray-400 mt-1">
                <span>0</span>
                <span>40</span>
                <span>100</span>
              </div>
            </div>
          </div>
        </Card>
      </div>

      <!-- Right Panel -->
      <div class="space-y-4">
        <!-- Max Working Pressure -->
        <Card class="bg-gray-800 border-gray-700">
          <h3 class="text-gray-400 text-sm mb-2">Max Working Pressure with HS88</h3>
          <div class="text-white text-4xl font-bold">{maxWorkingPressure}</div>
          <div class="text-gray-400 text-sm">max psi</div>
        </Card>

        <!-- Differential Adjustment -->
        <Card class="bg-gray-800 border-gray-700">
          <h3 class="text-gray-400 text-sm mb-2">Differential Adjustment</h3>
          <div class="text-white text-4xl font-bold">{differentialAdjustment}</div>
        </Card>

        <!-- Estimated Off-Bottom Pressure -->
        <Card class="bg-gray-800 border-gray-700">
          <h3 class="text-gray-400 text-sm mb-2">Estimated Off-Bottom Pressure</h3>
          <div class="text-white text-4xl font-bold">{estimatedPressure}</div>
          <div class="text-gray-400 text-sm">max psi</div>
        </Card>

        <!-- Available Diff -->
        <Card class="bg-gray-800 border-gray-700">
          <h3 class="text-gray-400 text-sm mb-2">Available Diff after Temp and Fluid Effects</h3>
          <div class="text-white text-4xl font-bold">{availableDiff}</div>
          <div class="text-gray-400 text-sm">psi</div>
        </Card>
      </div>
    </div>

    <!-- Generate PDF Button -->
    <div class="mt-6">
      <Button color="blue" on:click={handleGeneratePDF}>
        <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
        </svg>
        Generate PDF
      </Button>
    </div>
  </div>
</div>