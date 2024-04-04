    <!-- EventModal.vue -->
    <template>
        <div class="modal" v-if="visible" @click.self="$emit('close')">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">일정 추가</h5>
                <button type="button" class="close" aria-label="Close" @click="$emit('close')">
                <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div class="modal-body">
                <input type="text" v-model="newEventTitle" class="form-control" placeholder="최대 10자 입력 가능">
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" @click="$emit('close')">취소</button>
                <button type="button" class="btn btn-primary" @click="saveEvent">저장</button>
            </div>
            </div>
        </div>
        </div>
    </template>
    
    <script>
    export default {
        props: ['visible'],
        data() {
        return {
            newEventTitle: ''
        };
        },
        methods: {
        saveEvent() {
            this.$emit('save', this.newEventTitle);
        }
        }
    };
    </script>
    
    <style>
    /* Modal Styles */
    .modal {
        display: flex;
        align-items: center;
        justify-content: center;
        position: fixed;
        z-index: 1050;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        overflow: auto;
        outline: 0;
        background-color: rgba(0, 0, 0, 0.5); /* 배경에 흐릿하게 나타나도록 */
    }
    
    .modal-dialog {
        position: relative;
        width: auto;
        margin: 10px;
    }
    
    .modal-content {
        position: relative;
        background-color: #fff;
        border: 1px solid rgba(0, 0, 0, 0.2);
        border-radius: 0.3rem;
        outline: 0;
    }
    
    .modal-header {
        padding: 15px;
        border-bottom: 1px solid #e9ecef;
    }
    
    .modal-body {
        position: relative;
        padding: 15px;
    }
    
    .modal-footer {
        padding: 15px;
        text-align: right;
        border-top: 1px solid #e9ecef;
    }
    </style>
    