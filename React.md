//阻止表单提交
handleSubmit = (event)=>{
  event.preventDefault()
}

//form表单提交事件
<form onSubmit={this.handleSubmit}></form>

//设置回调函数ref
<input ref={c => this.username = c} />

//获取回调函数ref
handleSubmit = ()=>{
  const {username} = this
}
