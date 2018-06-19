<template>
    <div>
        <div class="container">
            <h3>Introduceti numarul care doriti sa fie permutat:</h3>
            <br>
            <input type="text" class="form-control" id="exampleFormControlInput2" v-model="number"
                   placeholder="Introduceti numarul:">
            <br>
            <button type="button" class="btn btn-secondary" @click="permutari(number)">Permuta!</button>
            <br><br>
            <div v-if="solutiiFinale.length">
                <h3>Permutarile sunt:</h3>
                <br>
                {{ solutiiFinale }}
            </div>
            <br>
        </div>
    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                number: '',
                k: 0,
                valid: false,
                solutii: [],
                solutiiFinale: [],
            }
        },
        methods: {
            permutari: function (n) {
                for (let i = 0; i < n; i++) {
                    this.solutii[i] = 0;
                }

                while (this.k >= 0) {
                    this.solutii[this.k]++;
                    this.valid = false;

                    while (!this.valid && this.solutii[this.k] <= n) {
                        if (this.ver(this.solutii, this.k + 1)) {
                            this.valid = true;
                        } else {
                            this.solutii[this.k]++;
                        }
                    }

                    if (this.valid) {
                        if (this.k == n - 1) {
                            console.log(this.solutii);
                            this.solutiiFinale.push(this.solutii.slice(0));
                        } else {
                            this.k++;
                            this.solutii[this.k] = 0;
                        }

                    } else {
                        this.k--;
                    }

                }

            },
            ver: function (array, k) {
                for (let i = 0; i < k - 1; i++) {
                    for (let j = i + 1; j < k; j++) {
                        if (array[i] == array[j]) {
                            return false;
                        }
                    }
                }
                return true;
            }
        }
    }
</script>

<style lang="scss">

</style>