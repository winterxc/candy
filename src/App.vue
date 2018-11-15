<template>
	<golden-layout style="width:100%;height:100%;" :has-headers="false" :border-width="2">
		<gl-row>
			<gl-component :width="20">
				xxx
			</gl-component>
			<gl-component>
				<golden-layout style="width:100%;height:100%;" :has-headers="true" :show-popout-icon="false" :border-width="2">
					<template slot="box" slot-scope="{i}">
						<editor v-model="home" :options="editorOptions" height="100%" preview-style="vertical" mode="wysiwyg" />
					</template>
					<gl-stack>
						<gl-component v-for="i in [1,2,3,4]" :key="i" :title="'Test' + i" template="box" :state="{i}"/>
					</gl-stack>
				</golden-layout>
			</gl-component>
		</gl-row>
	</golden-layout>
</template>
<script>
import Vue from 'vue'
import 'golden-layout/src/css/goldenlayout-light-theme.css'
import 'tui-editor/dist/tui-editor.css';
import 'tui-editor/dist/tui-editor-contents.css';
import 'codemirror/lib/codemirror.css';
import { Editor , Viewer} from '@toast-ui/vue-editor'
import 'tui-editor/dist/tui-editor-extChart.js';//chart
import 'tui-editor/dist/tui-editor-extScrollSync.js';//scrollSync
import 'tui-editor/dist/tui-editor-extUML.js';//uml
import 'tui-editor/dist/tui-editor-extColorSyntax.js';//colorSyntac
import 'tui-editor/dist/tui-editor-extTable.js';//table
import vgl from 'vue-golden-layout'
Vue.use(vgl);

export default {
	components: {editor: Editor, viewer: Viewer},
	data: function(){
		return {
			home: "Home",
			editorOptions: {
				exts: ['chart', 'uml', 'scrollSync', 'colorSyntac', 'table']
			}
		}
	}
}
</script>
<style lang="less">
.glComponent {
	width: 100%;
	height: 100%;
	overflow: auto;
	.tui-editor-defaultUI {
		border-width: 0;
	}
	.lm_header .lm_tab {
		background: #e3e3e3;
		&:hover, &.lm_active {
			background: white;
		}
	}
	.lm_content {
		background: white;
	}
}
</style>
