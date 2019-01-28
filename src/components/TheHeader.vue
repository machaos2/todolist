<template>
	<div class="todo">
		<h1>Todo List</h1>
		<div class="todolistBody">
			<input type="text" class="startInput" placeholder="What needs to be done?" autofocus="autofocus" v-model="task.content" @keydown.enter="addtask"/>
			<ul class="allThings" v-if="list.length !== 0">
				<li v-for="(task,index) in list">
					<label>
						<input type="checkbox" @click="changeState(index)" :checked="task.finished"/>
						<span :class="{finish:task.finished}">{{task.content}}</span>
					</label>
					<button @click="deleteTask(index)">删除</button>
				</li>
			</ul>
			<p class="showTip" v-if="list.length === 0">暂无数据</p>
		</div>
	</div>
</template>

<script>
	import ls from '../utils/localStorage'
	export default{
		name:'TheHeader',
		data(){
			return{
				task:{
					content:'',
					finished:false
				},
				list:[]
			}
		},
		mounted(){
			
			var getmsg = ls.getItem("list");
			console.log(getmsg);
			if(getmsg == '' || !getmsg || getmsg == null){
				ls.setItem("list",this.list);
			}
			getmsg = ls.getItem("list");
			this.list = getmsg;
		},
		watch:{
			list:{
				handler:function(){
					ls.setItem('list',this.list);
				}
			}
		},
		methods:{
			addtask(){
				if(this.task.content == ""){
					return false;
				}
				this.list.push(this.task);
				this.task = {
					content:'',
					finished:false
				};
				ls.setItem("list",this.list);
			},
			deleteTask(index){
				this.list.splice(index,1);
			},
			changeState(index){
				let onstate = this.list[index].finished;
				this.list[index].finished = !onstate;
				ls.setItem('list',this.list);
			}
		}
	}
</script>

<style scoped>
	.todo{text-align: left;width: 600px;margin: 0 auto;background: #eee;padding: 20px;}
	h1{text-align: center;text-transform: uppercase;color: #0285D3;margin-bottom: 20px;}
	.todolistBody{width: 500px;margin: 0 auto;}
	.finish{text-decoration: line-through;color: #ccc;}
	.startInput{border: 2px solid #0285d3;width: 476px;height: 36px;padding: 10px;font-size: 20px;}
	.allThings{padding: 20px;border: 1px solid #cccaca;background: #fff;box-shadow: 0 0 5px #ccc;}
	.allThings li{font-size: 20px;height: 40px;line-height: 40px;border-bottom: 1px solid #ededed;}
	.allThings li label{user-select: none;display: inline-block;width: 400px;}
	.allThings li button{background: #ac0b17;color: #fff;font-size: 20px;padding: 5px;border-radius: 8px;}
	.showTip{padding: 20px;font-size: 20px;}
</style>