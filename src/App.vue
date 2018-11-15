<template>
	<golden-layout style="width:100%;height:100%;" :has-headers="false" :border-width="2">
		<gl-row>
			<gl-component :width="20" style="background-color:#F3F3F3;">
				<multiselect v-model="query" :options="queryOptions" 
					tag-placeholder="Add this as new tag"
					placeholder="Search or add a tag" 
	  				label="Query" 
					:multiple="true"
	   				track-by="code"
	   				@tag="addTag"
					:taggable="true"></multiselect>
			</gl-component>
			<gl-component>
				<golden-layout style="width:100%;height:100%;" :has-headers="true" :show-maximise-icon="false" :show-popout-icon="false" :border-width="2">
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
import 'tui-editor/dist/tui-editor.css'
import 'tui-editor/dist/tui-editor-contents.css'
import 'codemirror/lib/codemirror.css'
import 'vue-multiselect/dist/vue-multiselect.min.css'
import { Editor , Viewer} from '@toast-ui/vue-editor'
import Multiselect from 'vue-multiselect'
import 'tui-editor/dist/tui-editor-extChart.js'
import 'tui-editor/dist/tui-editor-extScrollSync.js'
import 'tui-editor/dist/tui-editor-extUML.js'
import 'tui-editor/dist/tui-editor-extColorSyntax.js'
import 'tui-editor/dist/tui-editor-extTable.js'
import vgl from 'vue-golden-layout'
Vue.use(vgl);

export default {
	components: {editor:Editor, viewer:Viewer, multiselect:Multiselect},
	data: function(){
		return {
			home: "Home",
			query: [{ name: 'Javascript', code: 'js' }],
			queryOptions: [
				{ name: 'Vue.js', code: 'vu' },
        		{ name: 'Javascript', code: 'js' },
        		{ name: 'Open Source', code: 'os' }
			],
			editorOptions: {
				exts: ['chart', 'uml', 'scrollSync', 'colorSyntac', 'table']
			}
		}
	},
	methods: {
		addTag: function(newTag){
			let tag = {
				name: newTag, 
				code: newTag
			};
			this.query.push(tag)
			this.queryOptions.push(tag)
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
		background: #F3F3F3;
	}
	.lm_header .lm_tab {
		background: #F3F3F3;
		&:hover, &.lm_active {
			background: white;
		}
	}
	.lm_content {
		background: white;
	}
}
</style>
