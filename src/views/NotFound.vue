<template>
  <div class="flex flex-center bg-grey-2" style="min-height: 100vh;">
    <div class="text-center q-pa-md">
      <q-icon 
        name="search_off" 
        size="120px" 
        color="warning"
        class="q-mb-md"
      />
      
      <div class="text-h3 text-weight-bold text-grey-8 q-mb-md">
        404
      </div>
      
      <div class="text-h5 text-grey-7 q-mb-md">
        Página No Encontrada
      </div>
      
      <div class="text-body1 text-grey-6 q-mb-xl" style="max-width: 400px;">
        Lo sentimos, la página que buscas no existe o ha sido movida.
        Verifica la URL o regresa al inicio.
      </div>
      
      <div class="q-gutter-sm">
        <q-btn
          label="Ir al Inicio"
          color="primary"
          unelevated
          size="md"
          @click="goToHome"
          icon="home"
        />
        
        <q-btn
          label="Volver Atrás"
          color="primary"
          outline
          size="md"
          @click="goBack"
          icon="arrow_back"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { useRouter } from 'vue-router'

export default {
  name: 'NotFoundView',
  
  setup() {
    const router = useRouter()
    
    const goToHome = () => {
      const userRole = localStorage.getItem('userRole')
      const token = localStorage.getItem('authToken')
      
      if (!token) {
        router.push('/')
        return
      }
      
      if (userRole === 'admin') {
        router.push('/app/inicio')
      } else if (userRole === 'instructor') {
        router.push('/app/instructor/bitacoras')
      } else if (userRole === 'aprendiz') {
        router.push('/app/aprendiz/inicio')
      } else {
        router.push('/')
      }
    }
    
    const goBack = () => {
      router.go(-1)
    }
    
    return {
      goToHome,
      goBack
    }
  }
}
</script>

<style scoped>
.flex {
  display: flex;
}

.flex-center {
  justify-content: center;
  align-items: center;
}

.bg-grey-2 {
  background-color: #fafafa;
}
</style>