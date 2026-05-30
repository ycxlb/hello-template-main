# Hello main Templates

一组实用的 Home Assistant Jinja2 模板宏，封装常用计算和格式化逻辑。

## 安装

### 通过 HACS（需开启实验性功能）
1. HACS → 设置 → 开启**实验性功能**
2. 自定义仓库 → 添加 URL为(  https://github.com/ycxlb/hello-template-main  )，类别选择 **Template**
3. 安装后调用服务 `homeassistant.reload_custom_templates`

### 手动安装
1. 复制 `hello_main.jinja` 文件到 `config/custom_templates/`
2. 调用服务 `homeassistant.reload_custom_templates`

## 使用方法

在模板传感器或卡片配置中：

{% from 'utils.jinja' import format_duration, electricity_total %}

{# 格式化持续时间 #}
{{ format_duration(3665) }}  {# 输出：1小时1分 #}

{# 计算电费 #}
{{ electricity_total(states('sensor.nordpool_price'), 0.05, 0.02) }}

{# 状态徽章 #}
{{ state_badge('binary_sensor.door', '开门', '关门') }}

宏名	用途	参数

format_duration(seconds)	格式化秒数为易读时间	seconds: 秒数

electricity_total(spot_price, transport, broker, vat)	计算含附加费的电价	spot_price: 现货价, transport: 输电费, broker: 经纪费, vat: 增值税率

state_badge(entity_id, on_text, off_text)	状态彩色徽章	entity_id: 实体ID

range_color(value, min_val, max_val)	根据数值范围返回颜色	value: 当前值, min/max: 范围
