<h1 align="center">FACE-SDF</h1>

<div align="center">


![Static Badge](https://img.shields.io/badge/gdscript-blue?logo=godotengine&logoColor=white)

</div>

## 介绍
<br>动漫脸部阴影着色器，使用参考案例/教程翻译至Godot着色器。

<br>尝试将Unity的着色器代码/可视化着色器翻译至Godot着色器。
<br>参考了一些示例，并且将可能遇到的问题进行改进。
<br>https://youtu.be/WR_SP4LmOlw?si=lfh9Zi-sJM4t0VjC
<br>https://youtu.be/LKR1ITdOeKM?si=Nh6wvRhcAA4_7p6M
<br>尽管如此，这个着色器仍然有许多问题。

## 问题
<br>1.点光的阴影方向可能不太准确。
<br>2.目前暂无办法将阴影平滑过渡，可能需要更多的研究。
<br>3.阴影的过渡速度稍快。
<br>4.提示：如果必须应用到你的游戏项目，请仔细阅读该着色器目前遇到的问题。

## 修改
<br>1.转换了3D空间使其兼容。
<br>2.颜色着色器方面进行了细微修改。

## 使用提示
<br>1.需要一个SDF图片和模型的颜色图片。
<br>2.需要一个专门处理脸部的材质槽，并且带UV。
<br>3.为了阴影精准投射，需要加入以下代码：
```gdscript
func physics_process(delta):
	body_mesh.get_surface_override_material(0).set("shader_parameter/forward", Vector3.FORWARD *  self.transform.origin)
	body_mesh.get_surface_override_material(0).set("shader_parameter/right", Vector3.RIGHT * self.transform.origin)
```
<br>    建议添加Marker3D以对准向量。
<br>4.如果出现阴影从相反的方向投射，请直接用减法反转，例如：
```
    Vector3.RIGHT * -self.transform.origin
```

## 着色器参数
`Base Texture` 彩色底图，即模型原来绘画的颜色
`Color` 颜色，混合彩色底图
`Shadow` 阴影颜色
`Forward` 向前向量，用于对准向前坐标，通常是 z = 1.0。
`Right` 向右向量，用于对准向右坐标，通常是 x = 1.0。
`SDF` SDF贴图，必须由自己在模型绘画并生成。