<template>
        <div>
        <svg 
            id="drawSvg" 
            class="box"
            ref="box"       
            width="500" height="300"
            viewBox="0 0 163.56 89.921"
            @click="onClick"
            >
        <g transform="translate(-15.303 -12.363)" stroke="#4d4d4d" stroke-width="3.5325">
        <rect x="17.07" y="14.13" width="160.03" height="86.389" ry="0" fill="#f2f2f2" fill-rule="evenodd" stroke-linecap="round"/>
        <g fill="none">
        <path d="m112.43 14.366v15.578"/>
        <path d="m112.43 49.063v51.928"/>
        <path d="m77.731 14.838v43.43h-11.566"/>
        <path d="m60.5 58.032h-11.094v-43.43"/>
        <path d="m49.643 74.319v25.492"/>
        <path d="m18.486 58.74h18.175"/>
        </g>

        <g id="points-list" >
        </g>
        <g v-for="(point, index) in points" 
            :key="index+'string'">
        <circle  
            :cx="point.x" :cy="point.y" 
            r="3" 
            stroke="#AD2828"  
            stroke-width="3" 
            fill="#AD2828"  />
        <text  :x="point.x-1.3" :y="point.y+1.8" stroke="none" fill="#fff" font-size="5" >{{index}}</text>
        </g>

        </g>
        </svg>
        <button @click="handleButton">CLICK ME</button>
        </div>

        
</template>

<script>

export default {
    name: "human-plan",
    data() {
        return{
            board: '',
            circle: false,
            viewbox: null,
            square: {
                x: 35,
                y: 35,
            },
            points: [ 
                {"x":145,"y":60},
                {"x":95,"y":43}    
            ],
            dragOffsetX: null,
            dragOffsetY: null,
            svg:null,
            pt:null
        }
    },
    computed:{
        canvasWidth: function(){
            return this.board.clientWidth
        },

        canvasHeight: function(){
            return this.board.clientHeight
        },
        circleExist(){
            return this.circle;
        },
        viewboxText(){
            //`0 0 92.604 50.91`
            return `0 0 ${this.board.clientWidth} ${this.board.clientHeight}` 
        },
    },
    methods:{
        initBoard: function(){
            this.svg = document.getElementById("drawSvg");
            this.pt = this.svg.createSVGPoint();
            this.board = document.getElementById("drawSvg")
            this.viewbox = document.getElementById("drawSvg").viewBox.baseVal;
            console.log(this.viewbox)

        },
        handleButton(){
            console.log("POPULATE")
            //this.points.forEach(e =>{
            //    document.getElementById("points-list").appendChild(e)
            //    });
            
        },
        onClick(e){            
            
            this.pt.x = e.clientX+45;
            this.pt.y = e.clientY+45;
            var cursorpt =  this.pt.matrixTransform(this.svg.getScreenCTM().inverse());
            
            let path = document.createElementNS('http://www.w3.org/2000/svg','circle');
            path.setAttributeNS(null,'cx',cursorpt.x);
            path.setAttributeNS(null,'cy',cursorpt.y);
            path.setAttributeNS(null,'r','1');
            path.setAttributeNS(null,'fill','#444');
            path.setAttributeNS(null,'stroke','#333');
            path.setAttributeNS(null,'fill-rule','evenodd');
            path.setAttributeNS(null,'stroke-linecap','round');
            console.log(path)
            //document.getElementById("points-list").appendChild(path);
            this.points.push({"x": cursorpt.x ,"y": cursorpt.y});
            console.log(this.points);
        },
        
        showPoint(point){
            console.log("P>:",point);
            return point;
        },
        serializeObject(o){
            var s= new XMLSerializer();
            var parser = new DOMParser();
            return parser.parseFromString( s.serializeToString(o), "image/svg+xml");
            
        }
    
    },
    created(){
        
    },
    mounted(){
        this.initBoard();
        this.handleButton();
    }
        
    
}
</script>

<style lang="scss" scoped>
    .box{
        margin: auto;
        position: center;
        display: block; 
    }

</style>



