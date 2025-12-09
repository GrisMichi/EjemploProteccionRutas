<template>
  <div class="flex flex-center bg-grey-2" style="min-height: 100vh;">
    <div class="text-center q-pa-md">
      <q-icon 
        name="block" 
        size="120px" 
        color="negative"
        class="q-mb-md"
      />
      
      <div class="text-h3 text-weight-bold text-grey-8 q-mb-md">
        403
      </div>
      
      <div class="text-h5 text-grey-7 q-mb-md">
        Acceso No Autorizado
      </div>
      
      <div class="text-body1 text-grey-6 q-mb-xl" style="max-width: 400px;">
        No tienes los permisos necesarios para acceder a esta página.
        Por favor contacta al administrador si crees que esto es un error.
      </div>
      
      <div class="q-gutter-sm">
        <q-btn
          label="Volver al Inicio"
          color="primary"
          unelevated
          size="md"
          @click="goToHome"
          icon="home"
        />
        
        <q-btn
          label="Cerrar Sesión"
          color="negative"
          outline
          size="md"
          @click="logout"
          icon="logout"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { useRouter } from 'vue-router'
import { useQuasar } from 'quasar'

export default {
  name: 'UnauthorizedView',
  
  setup() {
    const router = useRouter()
    const $q = useQuasar()
    
    const goToHome = () => {
      const userRole = localStorage.getItem('userRole')
      
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
    
    const logout = () => {
      localStorage.removeItem('authToken')
      localStorage.removeItem('userRole')
      
      $q.notify({
        type: 'info',
        message: 'Sesión cerrada correctamente',
        position: 'top'
      })
      
      router.push('/')
    }
    
    return {
      goToHome,
      logout
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