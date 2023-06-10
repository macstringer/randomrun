

<template>
    <div>
        <canvas ref="canvas" width="400" height="400"></canvas>
        <p>{{ myPoints }}</p>
        <p>{{ rotatedPoints }}</p>
        <div id="map"></div>
    </div>
</template>

<script>


export default {
    name: 'PolygonDrawer',
    data() {
        return {
            myPoints: String,
            rotatedPoints: String
        };
    },
    mounted() {
        let points = this.generatePointArray(9, 400, 400);
        this.polySort(points)
        let rotPoints = [...points];
        this.rotateArray(rotPoints);
        this.myPoints = points
        this.rotatedPoints = rotPoints
        this.drawPolygon(points)







    },
    methods: {
        generatePoint(xBound, yBound) {
            let maxX = Math.floor(xBound);
            let maxY = Math.floor(yBound);

            let x = Math.floor(Math.random() * (maxX + 1));
            let y = Math.floor(Math.random() * (maxY + 1));

            return [x, y];
        },
        generatePointArray(amount, xDimension, yDimension) {
            let myArray = [];
            for (let i = 0; i < amount; i++) {
                myArray.push(this.generatePoint(xDimension, yDimension))
            }
            return myArray;
        },
        squaredPolar(point, center) {
            return [
                Math.atan2(point[1] - center[1], point[0] - center[0]),
                (point[0] - center[0]) ** 2 + (point[1] - center[1]) ** 2 // Square of distance
            ];
        },
        polySort(points) {
            // average all of the points
            let center = [points.reduce((sum, p) => sum + p[0], 0) / points.length,
            points.reduce((sum, p) => sum + p[1], 0) / points.length];
            // sort by polar angle and distance, centered at this center of mass
            for (let point of points) point.push(...this.squaredPolar(point, center));
            points.sort((a, b) => a[2] - b[2] || a[3] - b[3]);
            // throw away the temporary polar coordinates
            for (let point of points) point.length -= 2;
        },
        drawPolygon(points) {
            const canvas = document.getElementById("canvas");
            const ctx = canvas.getContext("2d");
            console.log(ctx)
            ctx.strokeStyle = "black";
            ctx.beginPath();
            ctx.moveTo(points[0][0], points[0][1]);
            for (let i in points) {
                console.log(points[i])
                ctx.lineTo(points[i][0], points[i][1]);
            }
            ctx.closePath();
            ctx.stroke();
        },
        rotateArray(array) {
            let max = array.length;
            let rotateAmount = Math.floor(Math.random() * (max + 1));
            for (let i = 0; i < rotateAmount; i++) {
                array.push(array.shift())
            }
        }

    },
    computed: {
        // Component computed properties go here
    },
    created() {
        // Component initialization code goes here
    },
    // Other lifecycle hooks and component options can be added here
};
</script>

<style scoped>
/* Component-specific styles go here */
</style>
