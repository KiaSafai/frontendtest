<template>
    <div class="container">
        <div class="chessboard">
            <div v-for="(file, fileIndex) in files" :key="file"> 
                <div  v-for="(rank, rankIndex) in ranks" :key="rank" :class = "getColor(rankIndex, fileIndex + 1)" @click="highlight(fileIndex + 1, rankIndex)"> 
                    {{file}}{{ rank }}
                </div>       
            </div>
        </div>
        <div class="sidebar">
            <div>Sidebar:</div>
            <div v-for="(square, index) in squareArray" :key = index>
                {{ index + 1 }}. {{ square }}
            </div>
        </div>
    </div> 
    

</template>

<script>
    export default {
        data() {
            //here we create the basis for each square to be used in the nested "v-for" loops above
            return {
                files: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'],
                ranks: ['8', '7', '6', '5', '4', '3', '2', '1'],
                clickedSquare: null,
                squareArray: []
            }
        },
        methods: {
            //here we determine if the square is light, dark, or highlighted
            getColor(rank, file) {
                if (JSON.stringify(this.clickedSquare) == JSON.stringify([file, rank])) {
                    return 'clickedSquare';
                } else if ((file + rank) % 2 == 0) {
                    return 'darkSquare';
                } else {
                    return 'lightSquare';
                }
            },
            //this is the method called onClick
            highlight(file, rank) {
                this.clickedSquare = [file, rank];
                this.squareArray.push(this.files[file - 1] + this.ranks[rank]);
            }
        },
        name: 'Chessboard'
    }
</script>