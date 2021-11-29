# cesium-tilesetEffect
基于3dtileset的特效

----------------------------------------------------------------------------------------------------------------------------------------
### 基于cesium的3dtilset模型特效
### cesium-tilesetEffect

### 说明
##### /cesium-tilesetEffect/src/doc

### 使用

#####  在项目中引入Cesium.js

#####  然后引入 cesium-tilesetEffect.js 即可


<a href="http://zhangticcc.gitee.io/webgis/"><img alt="" height="100%" src="https://img-blog.csdnimg.cn/20201127105619745.gif" width="90%" ></a>&nbsp;

```
      // 特效 默认开启
      Cesium.TILE_EFFECT_STATE = true;
 
      // 片元着色器 默认 可以自定义
      Cesium.TILE_FS_BODY = ` float stc_pl = fract(czm_frameNumber / 120.0) * 3.14159265 *         
                 2.0;
                float stc_sd = v_stcVertex.z / 60.0 + sin(stc_pl) * 0.1;
                gl_FragColor *= vec4(stc_sd, stc_sd, stc_sd, 1.0);
                float stc_a13 = fract(czm_frameNumber / 360.0);
                float stc_h = clamp(v_stcVertex.z / 450.0, 0.0, 1.0);
                stc_a13 = abs(stc_a13 - 0.5) * 2.0;
                float stc_diff = step(0.005, abs(stc_h - stc_a13));
                gl_FragColor.rgb += gl_FragColor.rgb * (1.0 - stc_diff);`;
                
      // 加载3dtileset
      let tilesets = viewer.scene.primitives.add(new Cesium.Cesium3DTileset({
        url: '/haidian/tileset.json'
      }))

      tilesets.readyPromise.then(function (tileset) {

        tileset.style = new Cesium.Cesium3DTileStyle({
          color: {
            conditions: [
              ["true", "color('cyan')"]
            ]
          }
        });

        viewer.flyTo(tileset)
      })
    }


```
