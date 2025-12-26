# Instrucciones para Configurar Contraseña Segura de Administrador

## Paso 1: Ejecutar el SQL en Supabase

1. Ve a tu proyecto en Supabase: https://supabase.com/dashboard
2. Navega a **SQL Editor**
3. Abre el archivo `admin-password-schema.sql`
4. Copia y pega todo el contenido en el editor SQL
5. Haz clic en **Run** para ejecutar el script

Esto creará la tabla `admin_password` e insertará el hash inicial de la contraseña `admin123`.

## Paso 2: Verificar que Funciona

1. Abre `http://localhost:8000/login-admin.html` en tu navegador
2. Ingresa la contraseña: `admin123`
3. Deberías poder acceder al panel de administración

## Paso 3: Cambiar la Contraseña (Opcional)

Si deseas cambiar la contraseña, puedes hacerlo de dos formas:

### Opción A: Desde el código (temporal)

Puedes crear un script temporal para actualizar la contraseña:

```javascript
// Ejecutar en la consola del navegador en login-admin.html
async function cambiarPassword() {
    await waitForSupabase();
    const nuevaPassword = prompt('Ingrese la nueva contraseña:');
    if (nuevaPassword) {
        const resultado = await actualizarPasswordAdmin(nuevaPassword);
        if (resultado) {
            alert('✅ Contraseña actualizada correctamente');
        } else {
            alert('❌ Error al actualizar contraseña');
        }
    }
}
cambiarPassword();
```

### Opción B: Directamente en Supabase

1. Ve a Supabase → **Table Editor** → `admin_password`
2. Calcula el hash SHA-256 de tu nueva contraseña (puedes usar una herramienta online como https://emn178.github.io/online-tools/sha256.html)
3. Actualiza el campo `password_hash` con el nuevo hash

## Seguridad

- ✅ La contraseña **NO** está visible en el código fuente
- ✅ Se almacena como hash SHA-256 en Supabase
- ✅ La validación se hace comparando hashes, no la contraseña en texto plano
- ⚠️ **Nota:** SHA-256 es seguro para este caso, pero para aplicaciones más críticas se recomienda usar bcrypt o Argon2

## Contraseña por Defecto

La contraseña inicial es: `admin123`

**IMPORTANTE:** Cambia esta contraseña después de la primera configuración.

