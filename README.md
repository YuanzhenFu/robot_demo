#1. init_session()
**功能**: 初始化会话状态  
**输入**: 无  
**输出**: 无  
备注: 创建11个session_state变量控制界面状态，包含json_data（处理后的网络数据）、show_left_panel（左侧面板显示状态）等

2. process_capability_data(raw_data)
**功能**: 原始数据转换  
**输入**:  
- raw_data: List[Dict] - 原始事件流JSON数组  
**输出**:  
python
{
  "nodes": List[Dict],  # 节点列表（含id/real_name/type等属性）
  "edges": List[Dict],  # 带权边列表（含source/target/time等）
  "min_timestamp": float,  # 最小时间戳
  "max_time": float      # 最大时间跨度
}

3. json_editor_component()
​​**功能**​​: 双栏JSON编辑器
​​**输入**​​: 无
​​**输出**​​: 无
​​备注​​: 通过st.session_state.raw_json传递数据，含实时语法高亮和错误校验

4. build_network_graph(data)
​​**功能**​​: 网络图构建
​​**输入**​​:图节点数据
data: Dict - process_capability_data的**输出**
​​**输出**​​:
nx.DiGraph - 带属性的有向图
​​节点属性​​:
label: 显示标签
real_name: 原始名称
node_type: capability/provider
color: 节点颜色
size: 节点尺寸

5. generate_network_graph(data)
​​**功能**​​: 网络可视化渲染
​​**输入**​​:
data: Dict - process_capability_data的**输出**
​​**输出**​​:
plt.Figure - Matplotlib图表对象
​​异常​​: 返回None时表示生成失败

6. plot_path(G, path, title)
​​**功能**​​: 路径高亮绘制
​​**输入**​​:
G: nx.DiGraph - 网络图
path: List[str] - 节点ID序列
title: str - 图表标题
​​**输出**​​: 无
​​效果​​: 在Streamlit中直接渲染路径图

7. path_analysis_panel()
​​**功能**​​: 路径分析控制面板
​​**输入**​​: 无
​​**输出**​​: 无
​​副作用​​: 更新st.session_state.path_results存储三种路径计算结果

8. main()
​​**功能**​​: 系统入口函数
​​**输入**​​: 无
​​**输出**​​: 无
